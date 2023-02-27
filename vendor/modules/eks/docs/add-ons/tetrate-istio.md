<!-- note marker start -->
NOTE: This repo contains only the documentation for the private BoltsOps repo code.
Original file: https://github.com/boltops-pro/terraspace-pro-eks/blob/master/vendor/modules/eks/docs/add-ons/tetrate-istio.md
The docs are publish so they are available for interested subscribers.
For access to the source code, you can become a BoltOps subscriber.
See: https://learn.boltops.com

<!-- note marker end -->

# Tetrate Istio Distro

[Tetrate Istio Distro](https://istio.tetratelabs.io/) is simple, safe enterprise-grade Istio distro.

This add-on is implemented as an external add-on. For detailed documentation and usage of the add-on please refer to the add-on [repository](https://github.com/tetratelabs/terraform-eksblueprints-tetrate-istio-addon).

## Example

Checkout the full [example](https://github.com/tetratelabs/terraform-eksblueprints-tetrate-istio-addon/tree/main/blueprints/getting-started).

## Usage

This step deploys the [Tetrate Istio Distro](https://istio.tetratelabs.io/) with default Helm Chart config

```hcl
  enable_tetrate_istio = true
```

Alternatively, you can override the helm values by using the code snippet below

```hcl
  enable_tetrate_istio = true

  # Optional fine-grained configuration

  tetrate_istio_distribution    = "TID"    # (default, Tetrate Istio Distro)
  tetrate_istio_version         = "1.12.2"
  tetrate_istio_install_base    = "true"   # (default, Istio `base` Helm Chart)
  tetrate_istio_install_cni     = "true"   # (default, Istio `cni` Helm Chart)
  tetrate_istio_install_istiod  = "true"   # (default, Istio `istiod` Helm Chart)
  tetrate_istio_install_gateway = "true"   # (default, Istio `gateway` Helm Chart)

  # Istio `base` Helm Chart config
  tetrate_istio_base_helm_config = {
    name = "istio-base"            # (default) Release name.
    repository = "https://istio-release.storage.googleapis.com/charts" # (default) Repository URL where to locate the requested chart.
    chart   = "base"               # (default) Chart name to be installed.
    version = "1.12.2"             # (default) The exact chart version to install.
    values  = []
  }

  # Istio `cni` Helm Chart config
  tetrate_istio_cni_helm_config = {
    name = "istio-cni"             # (default) Release name.
    repository = "https://istio-release.storage.googleapis.com/charts" # (default) Repository URL where to locate the requested chart.
    chart   = "cni"                # (default) Chart name to be installed.
    version = "1.12.2"             # (default) The exact chart version to install.
    values  = [yamlencode({
      "global" : {
        "hub" : "containers.istio.tetratelabs.com",
        "tag" : "1.12.2-tetratefips-v0",
      }
    })]
  }

  # Istio `istiod` Helm Chart config
  tetrate_istio_istiod_helm_config = {
    name = "istio-istiod"          # (default) Release name.
    repository = "https://istio-release.storage.googleapis.com/charts" # (default) Repository URL where to locate the requested chart.
    chart   = "istiod"             # (default) Chart name to be installed.
    version = "1.12.2"             # (default) The exact chart version to install.
    values  = [yamlencode({
      "global" : {
        "hub" : "containers.istio.tetratelabs.com",
        "tag" : "1.12.2-tetratefips-v0",
      }
    })]
  }

  # Istio `gateway` Helm Chart config
  tetrate_istio_gateway_helm_config = {
    name = "istio-ingress"         # (default) Release name.
    repository = "https://istio-release.storage.googleapis.com/charts" # (default) Repository URL where to locate the requested chart.
    chart   = "gateway"            # (default) Chart name to be installed.
    version = "1.12.2"             # (default) The exact chart version to install.
    values  = []
  }
```

### GitOps Configuration

The following properties are made available for use when managing the add-on via GitOps

```hcl
tetrateIstio = {
  enable = true
}
```

GitOps with ArgoCD Add-on repo is located [here](https://github.com/aws-samples/eks-blueprints-add-ons/blob/main/chart/values.yaml)
