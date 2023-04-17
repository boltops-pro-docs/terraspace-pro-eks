<!-- note marker start -->
NOTE: This repo contains only the documentation for the private BoltsOps repo code.
Original file: https://github.com/boltops-pro/terraspace-pro-eks/blob/master/docs/eks/aws-auth.md
The docs are publish so they are available for interested subscribers.
For access to the source code, you can become a BoltOps subscriber.
See: https://learn.boltops.com

<!-- note marker end -->

After deploying this stack, you'll need to allow the IAM role associated the pipeline to be able to deploy to the EKS cluster. Otherwise, you'll see an error like this:

> error: You must be logged in to the server (the server has asked for the client to provide credentials)
801

Recommend using the [krew](https://krew.sigs.k8s.io/) to install the [aws-auth](https://github.com/keikoproj/aws-auth) plugin to manage your EKS User and IAM roles.

Example:

    # set up ~/.kube/config
    aws eks update-kubeconfig --name dev-cluster
    # see current users
    kubectl aws-auth get
    # get the IAM role to use
    TS_APP=demo TS_ROLE=deploy terraspace output codebuild
    # add IAM role - without this role codebuild will fail with `aws eks update-kubeconfig` silently
    kubectl aws-auth upsert --mapusers --userarn arn:aws:iam::111111111111:role/demo-dev-codebuild --username demo-dev-codebuild --groups system:masters

You also probably want to add your IAM user also.

    # replace USERNAME with your IAM username
    kubectl aws-auth upsert --mapusers --userarn arn:aws:iam::111111111111:user/USERNAME --username USERNAME --groups system:masters

Note to remove a user

    kubectl aws-auth remove-by-username --username demo-dev-codebuild

Confirm the users have been added with:

    kubectl aws-auth get

Remember for the production EKS cluster you'll need to switch over to it. Here's an example of setting up both clusters and setting friendly contexts names with `kubectx`.

    aws eks update-kubeconfig --name dev-cluster
    kubectx dev-cluster=.
    aws eks update-kubeconfig --name prod-cluster
    kubectx prod-cluster=.
