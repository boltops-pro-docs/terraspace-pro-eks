<!-- note marker start -->
NOTE: This repo contains only the documentation for the private BoltsOps repo code.
Original file: https://github.com/boltops-pro/terraspace-pro-eks/blob/master/vendor/modules/eks/docs/add-ons/cert-manager-istio-csr.md
The docs are publish so they are available for interested subscribers.
For access to the source code, you can become a BoltOps subscriber.
See: https://learn.boltops.com

<!-- note marker end -->

# cert-manager-istio-csr

istio-csr is an agent that allows for Istio workload and control plane components to be secured using cert-manager.

For complete project documentation, please visit the [cert-manager documentation site](https://cert-manager.io/docs/usage/istio/).

## Usage

cert-manger-istio-csr can be deployed by enabling the add-on via the following.

```hcl
enable_cert_manager_istio_csr = true
```

### GitOps Configuration

The following properties are made available for use when managing the add-on via GitOps.

```

certManagerIstioCsr = {
  enable = true
}
```
