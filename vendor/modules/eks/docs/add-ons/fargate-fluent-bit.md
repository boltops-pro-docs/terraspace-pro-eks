<!-- note marker start -->
NOTE: This repo contains only the documentation for the private BoltsOps repo code.
Original file: https://github.com/boltops-pro/terraspace-pro-eks/blob/master/vendor/modules/eks/docs/add-ons/fargate-fluent-bit.md
The docs are publish so they are available for interested subscribers.
For access to the source code, you can become a BoltOps subscriber.
See: https://learn.boltops.com

<!-- note marker end -->

## Fluent Bit for Fargate

[Fluent Bit for Fargate](https://aws.amazon.com/blogs/containers/fluent-bit-for-amazon-eks-on-aws-fargate-is-here/) configures Fluent Bit to forward Fargate Container logs to CloudWatch.

### Usage

Fluent Bit for Fargate can be deployed by enabling the add-on via the following.

```hcl
enable_fargate_fluentbit = true
```
