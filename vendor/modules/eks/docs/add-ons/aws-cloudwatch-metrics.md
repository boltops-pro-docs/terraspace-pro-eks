<!-- note marker start -->
NOTE: This repo contains only the documentation for the private BoltsOps repo code.
Original file: https://github.com/boltops-pro/terraspace-pro-eks/blob/master/vendor/modules/eks/docs/add-ons/aws-cloudwatch-metrics.md
The docs are publish so they are available for interested subscribers.
For access to the source code, you can become a BoltOps subscriber.
See: https://learn.boltops.com

<!-- note marker end -->

# AWS CloudWatch Metrics

Use CloudWatch Container Insights to collect, aggregate, and summarize metrics and logs from your containerized applications and microservices. CloudWatch automatically collects metrics for many resources, such as CPU, memory, disk, and network. Container Insights also provides diagnostic information, such as container restart failures, to help you isolate issues and resolve them quickly. You can also set CloudWatch alarms on metrics that Container Insights collects.

Container Insights collects data as performance log events using embedded metric format. These performance log events are entries that use a structured JSON schema that enables high-cardinality data to be ingested and stored at scale. From this data, CloudWatch creates aggregated metrics at the cluster, node, pod, task, and service level as CloudWatch metrics. The metrics that Container Insights collects are available in CloudWatch automatic dashboards, and also viewable in the Metrics section of the CloudWatch console.

## Usage

[aws-cloudwatch-metrics](https://github.com/aws-ia/terraform-aws-eks-blueprints/tree/main/modules/kubernetes-addons/aws-cloudwatch-metrics) can be deployed by enabling the add-on via the following.

```hcl
enable_aws_cloudwatch_metrics = true
```

You can optionally customize the Helm chart that deploys `aws_cloudwatch_metrics` via the following configuration.

```hcl
  enable_aws_cloudwatch_metrics        = true
  aws_cloudwatch_metrics_irsa_policies = ["IAM Policies"]
  aws_cloudwatch_metrics_helm_config   = {
    name       = "aws-cloudwatch-metrics"
    chart      = "aws-cloudwatch-metrics"
    repository = "https://aws.github.io/eks-charts"
    version    = "0.0.7"
    namespace  = "amazon-cloudwatch"
    values     = [templatefile("${path.module}/values.yaml", {
      eks_cluster_id = var.addon_context.eks_cluster_id
    })]
  }
```

### GitOps Configuration

The following properties are made available for use when managing the add-on via GitOps.

```hcl
awsCloudWatchMetrics = {
  enable       = true
}
```
