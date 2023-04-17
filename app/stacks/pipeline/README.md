<!-- note marker start -->
NOTE: This repo contains only the documentation for the private BoltsOps repo code.
Original file: https://github.com/boltops-pro/terraspace-pro-eks/blob/master/app/stacks/pipeline/README.md
The docs are publish so they are available for interested subscribers.
For access to the source code, you can become a BoltOps subscriber.
See: https://learn.boltops.com

<!-- note marker end -->

# CodePipeline Stack

## How It Works

This Code Pipeline deploys our app by calling CodeBuild projects. It's designed to be used with the codebuild stack.

We first deploy the codebuild stack(s) that will be used in the pipeline. Example:

    TS_APP=demo TS_ROLE=deploy terraspace up codebuild # creat demo-deploy-dev codebuild project

We use the codebuild project as a **stage** in this pipeline.

    source -> codebuild: demo-deploy-dev (deploys)

To create the pipeline

    unset TS_ROLE # Do not set for the pipeline
    TS_APP=demo terraspace up pipeline # create demo-dev pipeline

Note, make sure `TS_ROLE` is not set since we could add multiple codebuild stages (with different TS_ROLE) in one `TS_APP` pipeline. The pipeline is a higher level system that glues the codebuild components together.

## Configure

Configure TS_APP=demo specific tfvars variables. We'll surface some examples values to help see how things fit together.

The `base.tfvars` has common source options across all apps.

app/stacks/pipeline/tfvars/base.tfvars

    source_primary_full_repository_id   = "boltops-pro/codebuild-kubes"
    source_secondary_full_repository_id = "boltops-pro/demo-apps"

The `demo/dev.tfvars` has app-specific variables.

app/stacks/pipeline/tfvars/demo/dev.tfvars

    name                                = "demo-dev"
    codebuild_project_name_deploy       = "demo-deploy-dev"

## Deploy

    unset TS_ROLE # Do not set for the pipeline
    TS_APP=demo terraspace up pipeline # create demo-dev pipeline

A CodePipeline is created.

## GitHub Connection

Note, AWS CodePipeline immediately starts the first run of the pipeline upon creation. It will fail on the first run. This is because we'll need to approve the GitHub connection by connecting it your provider like GitHub.

To approve:

1. Go to the CodePipeline console on the botttom left-hand side under **Settings/Connections**. You should see a **Pending** github-connection. We created this when we ran `terraspace up pipeline`.
2. Click on it and then **Update Pending Connection**. This opens up a 3rd party window like GitHub. **Authorize AWS Connector for GitHub**. We recommend you use a bot GitHub account instead of a personal account.
3. Click **Install a new app** and select the GitHub organization so this specific AWS CodePipeline Connection is granted access to the organization's repos.

* AWS Docs: [Working with Connections](https://docs.aws.amazon.com/dtconsole/latest/userguide/connections.html)

## Release Pipeline

Go to the Pipeline console and click **Release**. The pipeline should now be able to download the source code and run the codebuild stage which deploys the app.
