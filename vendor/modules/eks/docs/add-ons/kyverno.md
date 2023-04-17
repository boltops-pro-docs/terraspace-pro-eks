<!-- note marker start -->
NOTE: This repo contains only the documentation for the private BoltsOps repo code.
Original file: https://github.com/boltops-pro/terraspace-pro-eks/blob/master/vendor/modules/eks/docs/add-ons/kyverno.md
The docs are publish so they are available for interested subscribers.
For access to the source code, you can become a BoltOps subscriber.
See: https://learn.boltops.com

<!-- note marker end -->

# Kyverno

Kyverno is a policy engine that can help kubernetes clusters to enforce security and governance policies.

This addon provides support for:
1. [Kyverno](https://github.com/kyverno/kyverno/tree/main/charts/kyverno)
2. [Kyverno policies](https://github.com/kyverno/kyverno/tree/main/charts/kyverno-policies)
3. [Kyverno policy reporter](https://github.com/kyverno/policy-reporter/tree/main/charts/policy-reporter)

## Usage

Kyverno can be deployed by enabling the respective add-on(s) via the following.

```hcl
enable_kyverno                 = true
enable_kyverno_policies        = true
enable_kyverno_policy_reporter = true
```

### GitOps Configuration

The following properties are made available for use when managing the add-on via GitOps.

```sh
kyverno = {
  enable = true
}

kyverno_policies = {
  enable = true
}

kyverno_policy_reporter = {
  enable = true
}
```
