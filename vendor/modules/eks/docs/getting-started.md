<!-- note marker start -->
NOTE: This repo contains only the documentation for the private BoltsOps repo code.
Original file: https://github.com/boltops-pro/terraspace-pro-eks/blob/master/vendor/modules/eks/docs/getting-started.md
The docs are publish so they are available for interested subscribers.
For access to the source code, you can become a BoltOps subscriber.
See: https://learn.boltops.com

<!-- note marker end -->

# Getting Started

This getting started guide will help you deploy your first EKS environment using EKS Blueprints.

## Prerequisites:

First, ensure that you have installed the following tools locally.

1. [aws cli](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html)
2. [kubectl](https://Kubernetes.io/docs/tasks/tools/)
3. [terraform](https://learn.hashicorp.com/tutorials/terraform/install-cli)

## Examples

Select an example from the [`examples/`](https://github.com/aws-ia/terraform-aws-eks-blueprints/tree/main/examples) directory and follow the instructions in its respective README.md file. The deployment steps for examples generally follow the deploy, validate, and clean-up steps shown below.

### Deploy

To provision this example:

```sh
terraform init
terraform apply -target module.vpc
terraform apply -target module.eks
terraform apply
```

Enter `yes` at command prompt to apply

### Validate

The following command will update the `kubeconfig` on your local machine and allow you to interact with your EKS Cluster using `kubectl` to validate the CoreDNS deployment for Fargate.

1. Run `update-kubeconfig` command:

```sh
aws eks --region <REGION> update-kubeconfig --name <CLUSTER_NAME>
```

3. View the pods that were created:

```sh
kubectl get pods -A

# Output should show some pods running
NAMESPACE     NAME                                  READY   STATUS    RESTARTS   AGE
kube-system   coredns-66b965946d-gd59n              1/1     Running   0          92s
kube-system   coredns-66b965946d-tsjrm              1/1     Running   0          92s
kube-system   ebs-csi-controller-57cb869486-bcm9z   6/6     Running   0          90s
kube-system   ebs-csi-controller-57cb869486-xw4z4   6/6     Running   0          90s
```

3. View the nodes that were created:

```sh
kubectl get nodes

# Output should show some nodes running
NAME                                                STATUS   ROLES    AGE     VERSION
fargate-ip-10-0-10-11.us-west-2.compute.internal    Ready    <none>   8m7s    v1.24.8-eks-a1bebd3
fargate-ip-10-0-10-210.us-west-2.compute.internal   Ready    <none>   2m50s   v1.24.8-eks-a1bebd3
fargate-ip-10-0-10-218.us-west-2.compute.internal   Ready    <none>   8m6s    v1.24.8-eks-a1bebd3
fargate-ip-10-0-10-227.us-west-2.compute.internal   Ready    <none>   8m8s    v1.24.8-eks-a1bebd3
fargate-ip-10-0-10-42.us-west-2.compute.internal    Ready    <none>   8m6s    v1.24.8-eks-a1bebd3
fargate-ip-10-0-10-71.us-west-2.compute.internal    Ready    <none>   2m48s   v1.24.8-eks-a1bebd3
```

### Destroy

To teardown and remove the resources created in this example:

```sh
terraform destroy -target="module.eks_blueprints_kubernetes_addons" -auto-approve
terraform destroy -target="module.eks" -auto-approve
terraform destroy -auto-approve
```
