<!-- note marker start -->
NOTE: This repo contains only the documentation for the private BoltsOps repo code.
Original file: https://github.com/boltops-pro/terraspace-pro-eks/blob/master/vendor/modules/eks/docs/add-ons/yunikorn.md
The docs are publish so they are available for interested subscribers.
For access to the source code, you can become a BoltOps subscriber.
See: https://learn.boltops.com

<!-- note marker end -->

# Apache YuniKorn
[YuniKorn](https://yunikorn.apache.org/) YuniKorn is a light-weight, universal resource scheduler for container orchestrator systems.

Apache YuniKorn (Incubating) is a new Apache incubator project that offers rich scheduling capabilities on Kubernetes. It fills the scheduling gap while running Big Data workloads on Kubernetes, with a ton of useful features such as hierarchical queues, elastic queue quotas, resource fairness, and job ordering

You can define `batchScheduler: "yunikorn"` when you are running Spark Applications using SparkK8sOperator

## Usage
This step deploys the Apache YuniKorn K8s schedular with default Helm Chart config

```hcl
  enable_yunikorn = true
```

Alternatively, you can override the helm values by using the code snippet below

```hcl
  enable_yunikorn = true

  yunikorn_helm_config = {
    name       = "yunikorn"                                 # (Required) Release name.
    repository = "https://apache.github.io/yunikorn-release" # (Optional) Repository URL where to locate the requested chart.
    chart      = "yunikorn"                                 # (Required) Chart name to be installed.
    version    = "0.12.2"                               # (Optional) Specify the exact chart version to install. If this is not specified, it defaults to the version set within default_helm_config: https://github.com/aws-ia/terraform-aws-eks-blueprints/blob/main/modules/kubernetes-addons/yunikorn/locals.tf
    values     = [templatefile("${path.module}/values.yaml", {})]
  }
```
