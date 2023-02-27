<!-- note marker start -->
NOTE: This repo contains only the documentation for the private BoltsOps repo code.
Original file: https://github.com/boltops-pro/terraspace-pro-eks/blob/master/app/stacks/codebuild/README.md
The docs are publish so they are available for interested subscribers.
For access to the source code, you can become a BoltOps subscriber.
See: https://learn.boltops.com

<!-- note marker end -->

# CodeBuild Stack

## How It Works

This CodeBuild project deploys your application. It makes use of multiple sources.

1. Infra: Centralized buildspec.yml and deploy/build.sh scripts
2. App: Specific App Source Code repo

This is done to minimize infrastructure code duplication. You'll centrally managed the infrastructure code and specify which app source code which be to used. The build script is a terraform variable so it's up to you if you want to use the same or different scripts for codebuild to run.

Depending on how different the scripts need to be, sometimes it makes sense to use the same script with conditional logic, and sometimes it makes sense to use completely separate script. Sometimes using a separate script starts let's you see the differences with more clarity and then you can re-factor and re-combine it to a single script when it's clear how to.

## Configure

Configure TS_APP=demo specific variables. Create these files and set their values.

* app/stacks/codebuild/tfvars/base.tfvars
* app/stacks/codebuild/tfvars/demo/dev.tfvars
* app/stacks/codebuild/tfvars/demo/deploy/dev.tfvars

The CodeBuild project makes use of 2 sources configured by variables `source_location` and `secondary_source_location`.

This is configured in `demo/base.tfvars` so we can use the same same source code

## Deploy

    export TS_APP=demo TS_ROLE=deploy
    terraspace up codebuild

The CodeBuild project is created named `demo-deploy-dev` and is set in `tfvars/demo/deploy/dev.tfvars` based on `TS_APP=demo TS_ROLE=deploy`.

It will use a build.sh script to deploy a demo app to EKS.

The CodeBuild hasn't been run yet. We'll do that soon after some more setup.

## CodeBuild Source Credentials

Codebuild will need a "source credential" in order to download source code from your private repositories. An example is an GitHub personal access token.

### Create the GitHub Oauth Token

Here are the steps to create a GitHub oauth token:

1. Go to GitHub Settings
2. Developer Settings
3. Personal access tokens

Important: Codebuild is limited to only allow a [single credential per given type and region]([https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/codebuild_source_credential) and is used by all the codebuild projects in that region. Because of this your token should have access to all the repositories you need. We'll also just manually import it since it's a one time task.

Create a file and replace `REPLACE_WITH_YOUR_TOKEN` with your GitHub User token.

codebuild-source-credentials.json

```json
{
  "token": "REPLACE_WITH_YOUR_TOKEN",
  "serverType": "GITHUB",
  "authType": "PERSONAL_ACCESS_TOKEN"
}
```

Then import your credential.

    aws codebuild import-source-credentials --cli-input-json file:///codebuild-source-credentials.json

You should see something like this:

    $ aws codebuild list-source-credentials
    {
      "sourceCredentialsInfos": [
        {
        "arn": "arn:aws:codebuild:us-west-2:111111111111:token/github",
        "serverType": "GITHUB",
        "authType": "PERSONAL_ACCESS_TOKEN"
        }
      ]
    }

Notice that the actual value is not shown and is not retrievable.

### Saving for the Future

We also recommend saving your token to ssm parameter store in case you need it in the future.

    TOKEN=REPLACE_WITH_YOUR_TOKEN
    # save
    aws ssm put-parameter --name /dev/GITHUB_TOKEN --type SecureString --value "$TOKEN"
    # to confirm
    aws ssm get-parameter --name /dev/GITHUB_TOKEN --with-decryption | jq -r '.Parameter.Value'

## EKS aws-auth permission

After deploying this stack, you'll need to allow the IAM role associated the pipeline to be able to deploy to the EKS cluster. Otherwise, you'll see an error like this:

> error: You must be logged in to the server (the server has asked for the client to provide credentials)
801

To add the role, replace the values with your value:

    terraspace output codebuild
    aws eks update-kubeconfig --name dev-cluster
    kubectl aws-auth get
    kubectl aws-auth upsert --mapusers --userarn arn:aws:iam::111111111111:role/demo-deploy-dev-codebuild --username demo-deploy-dev-codebuild --groups system:masters

More Docs: [EKS aws-auth](/docs/eks/aws-auth.md)

## SSM Parameters

The codebuild `buildspec.yml` calls a `build.sh` script that uses some environment variables with sensitive info. We'll store their values in SSM Parameters and CodeBuild will make them available as enviornment variables. These are in: `app/stacks/codebuild/tfvars/demo/dev.tfvars`

Create SSM Parameters for a docker login. You'll need a docker login to avoid hitting the DockerHub rate limit.  Here's a recommended naming pattern.

    /dev/DOCKER_USER
    /dev/DOCKER_PASS

And here's an example of creating a Parameter with the CLI. We recommend using a "bot" user account for this purpose.

    DOCKER_USER=REPLACE_WITH_YOUR_DOCKERHUB_USER
    aws ssm put-parameter --name /dev/DOCKER_USER --type String --value "$DOCKER_USER"
    aws ssm get-parameter --name /dev/DOCKER_USER --with-decryption | jq -r '.Parameter.Value'

    DOCKER_PASS=REPLACE_WITH_YOUR_DOCKERHUB_PASS
    aws ssm put-parameter --name /dev/DOCKER_PASS --type SecureString --value "$DOCKER_PASS"
    aws ssm get-parameter --name /dev/DOCKER_PASS --with-decryption | jq -r '.Parameter.Value'

You can also use the AWS Console to create the SSM Parameters instead.

## Create ECR Repo

You'll need to create an ECR repo so `kubes deploy` will be able to push the Docker image it builds to it.

    aws ecr create-repository --repository-name demo

## CodeBuild Start

Start CodeBuild Project run to

* In the console look for the **demo-deploy-dev** project
* Click on **Start Build**

You can also start the project with the cli:

    aws codebuild start-build --project-name demo-deploy-dev

Check the CodeBuild logs:

![](https://img.boltops.com/boltops-pro/terraspace/stacks/codebuild/demo-deploy-success.png)

## Additional Roles

If you need additional codebuild projects for different steps, like one for tests and one for deploy. You can use `TS_ROLE` which allows you to use different tfvar files. Here are some examples using this strategy:

### Example: tests role

For separate deploy tfvars:

    export TS_ROLE=deploy
    app/stacks/codebuild/tfvars/demo/deploy/dev.tfvars

For tests deploy tfvars:

    export TS_ROLE=tests
    app/stacks/codebuild/tfvars/demo/tests/dev.tfvars

### Example: web and worker roles

It is common to have a web and worker role or tier.  The web role is responsible for serving web traffic and the worker role is responsible for background job processing.  You can add use TS_ROLE to also handle this case also. Here are their corresponding roles and tfvars files.

    export TS_ROLE=deploy-web
    app/stacks/codebuild/tfvars/demo/deploy-web/dev.tfvars
    export TS_ROLE=deploy-worker
    app/stacks/codebuild/tfvars/demo/deploy-worker/dev.tfvars

To create the separate codebuild projects we would use:

    TS_APP=demo TS_ROLE=deploy-web    terraspace up # codebuild project: demo-deploy-web-dev
    TS_APP=demo TS_ROLE=deploy-worker terraspace up # codebuild project: demo-deploy-worker-dev

The TS_APP and TS_ROLE terraspace env vars and concepts allow you to use the same source code and build different stacks with different tfvars files.
