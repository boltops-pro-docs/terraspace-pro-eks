<!-- note marker start -->
NOTE: This repo contains only the documentation for the private BoltsOps repo code.
Original file: https://github.com/boltops-pro/terraspace-pro-eks/blob/master/vendor/modules/eks/docs/add-ons/kuberay-operator.md
The docs are publish so they are available for interested subscribers.
For access to the source code, you can become a BoltOps subscriber.
See: https://learn.boltops.com

<!-- note marker end -->

# KubeRay Operator

[KubeRay](https://github.com/ray-project/kuberay) is an open source toolkit to run [Ray](https://www.ray.io/) applications on Kubernetes. For details on its design, please refer to the KubeRay [documentation](https://ray-project.github.io/kuberay/).

> 🛑 This add-on should be considered as experimental and should only be used for proof of concept.


## Usage

KubeRay operator can be deployed by enabling the add-on via the following.

### Basic Example

```hcl
enable_kuberay_operator = true
```

### Advanced Example

Advanced example of KubeRay operator add-on is not currently supported as the upstream project does not publish a [Helm chart yet]. Please 👍 this [issue](https://github.com/ray-project/kuberay/issues/475).

### GitOps Configuration

GitOps is not currently supported due to lack of a published Helm chart upstream. Please 👍 this [issue](https://github.com/ray-project/kuberay/issues/475).
