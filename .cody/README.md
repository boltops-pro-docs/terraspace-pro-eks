<!-- note marker start -->
NOTE: This repo contains only the documentation for the private BoltsOps repo code.
Original file: https://github.com/boltops-pro/terraspace-pro-eks/blob/master/.cody/README.md
The docs are publish so they are available for interested subscribers.
For access to the source code, you can become a BoltOps subscriber.
See: https://learn.boltops.com

<!-- note marker end -->

# Cody Files

The files in folder are used by cody for AWS CodeBuild projects.  For more info: [Cody Docs](https://cody.run)

## Deploy CodeBuild Project

To deploy the CodeBuild project. IE: Create or update the CloudFormation stack.

Main services:

    cody up

If you have multiple codebuild projects associated with the same repo, you can use the `--type` option.  Example:

    cody up --type deploy

## Start a Deploy

To start a CodeBuild build:

    cody start
    cody start --type deploy

To specify a branch:

    cody start --type deploy --branch feature
