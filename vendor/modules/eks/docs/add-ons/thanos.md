<!-- note marker start -->
NOTE: This repo contains only the documentation for the private BoltsOps repo code.
Original file: https://github.com/boltops-pro/terraspace-pro-eks/blob/master/vendor/modules/eks/docs/add-ons/thanos.md
The docs are publish so they are available for interested subscribers.
For access to the source code, you can become a BoltOps subscriber.
See: https://learn.boltops.com

<!-- note marker end -->

# Thanos

Thanos is a highly available metrics system that can be added on top of existing Prometheus deployments, providing a global query view across all Prometheus installations.

For complete project documentation, please visit the [Thanos documentation site](https://thanos.io/tip/thanos/getting-started.md/).

## Usage

[Thanos](https://github.com/bitnami/charts/tree/main/bitnami/thanos) can be deployed by enabling the add-on via the following.

```hcl
enable_thanos = true
```

### GitOps Configuration

The following properties are made available for use when managing the add-on via GitOps

```
thanos = {
  enable = true
}
```
