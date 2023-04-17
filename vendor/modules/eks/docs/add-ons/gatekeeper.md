<!-- note marker start -->
NOTE: This repo contains only the documentation for the private BoltsOps repo code.
Original file: https://github.com/boltops-pro/terraspace-pro-eks/blob/master/vendor/modules/eks/docs/add-ons/gatekeeper.md
The docs are publish so they are available for interested subscribers.
For access to the source code, you can become a BoltOps subscriber.
See: https://learn.boltops.com

<!-- note marker end -->

# Gatekeeper

Gatekeeper is an admission controller that validates requests to create and update Pods on Kubernetes clusters, using the Open Policy Agent (OPA). Using Gatekeeper allows administrators to define policies with a constraint, which is a set of conditions that permit or deny deployment behaviors in Kubernetes.

For complete project documentation, please visit the [Gatekeeper](https://open-policy-agent.github.io/gatekeeper/website/docs/).
For reference templates refer [Templates](https://github.com/open-policy-agent/gatekeeper/tree/master/charts/gatekeeper/templates)

## Usage

Gatekeeper can be deployed by enabling the add-on via the following.

```hcl
enable_gatekeeper = true
```

You can optionally customize the Helm chart that deploys `Gatekeeper` via the following configuration.

```hcl
  enable_gatekeeper = true
  # Optional  gatekeeper_helm_config
  gatekeeper_helm_config = {
    name                       = "gatekeeper"
    chart                      = "gatekeeper"
    repository                 = "https://open-policy-agent.github.io/gatekeeper/charts"
    version                    = "3.9.0"
    namespace                  = "gatekeeper-system"
    values = [
      <<-EOT
        clusterName: ${var.eks_cluster_id}
      EOT
    ]
  }
```

### GitOps Configuration
The following properties are made available for use when managing the add-on via GitOps.

```hcl
  argocd_gitops_config = {
    enable          = true
    clusterName     = var.eks_cluster_id
  }
```
