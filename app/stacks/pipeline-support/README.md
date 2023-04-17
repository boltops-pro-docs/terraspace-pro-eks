<!-- note marker start -->
NOTE: This repo contains only the documentation for the private BoltsOps repo code.
Original file: https://github.com/boltops-pro/terraspace-pro-eks/blob/master/app/stacks/pipeline-support/README.md
The docs are publish so they are available for interested subscribers.
For access to the source code, you can become a BoltOps subscriber.
See: https://learn.boltops.com

<!-- note marker end -->

## Pipeline Support Shared Resources

* s3 bucket: So we can reuse the same bucket for multiple pipelines.
* codestar connection: So we can reuse the same connection for multiple pipelines.

## Deploy

    export TS_ENV=dev-shared
    terraspace up pipeline-support
