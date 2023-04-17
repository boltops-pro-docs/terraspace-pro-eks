<!-- note marker start -->
NOTE: This repo contains only the documentation for the private BoltsOps repo code.
Original file: https://github.com/boltops-pro/terraspace-pro-eks/blob/master/vendor/modules/eks/docs/advanced/private-clusters.md
The docs are publish so they are available for interested subscribers.
For access to the source code, you can become a BoltOps subscriber.
See: https://learn.boltops.com

<!-- note marker end -->

# Private Clusters

For fully Private EKS clusters requires the following VPC endpoints to be created to communicate with AWS services. This module will create these endpoints if you choose to create VPC. If you are using an existing VPC then you may need to ensure these endpoints are created.

    com.amazonaws.region.aps-workspaces            - For AWS Managed Prometheus Workspace
    com.amazonaws.region.ssm                       - Secrets Management
    com.amazonaws.region.ec2
    com.amazonaws.region.ecr.api
    com.amazonaws.region.ecr.dkr
    com.amazonaws.region.logs                       – For CloudWatch Logs
    com.amazonaws.region.sts                        – If using AWS Fargate or IAM roles for service accounts
    com.amazonaws.region.elasticloadbalancing       – If using Application Load Balancers
    com.amazonaws.region.autoscaling                – If using Cluster Autoscaler
    com.amazonaws.region.s3                         – Creates S3 gateway
