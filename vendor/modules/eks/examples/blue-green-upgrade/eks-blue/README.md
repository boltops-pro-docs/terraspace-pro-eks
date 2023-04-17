<!-- note marker start -->
NOTE: This repo contains only the documentation for the private BoltsOps repo code.
Original file: https://github.com/boltops-pro/terraspace-pro-eks/blob/master/vendor/modules/eks/examples/blue-green-upgrade/eks-blue/README.md
The docs are publish so they are available for interested subscribers.
For access to the source code, you can become a BoltOps subscriber.
See: https://learn.boltops.com

<!-- note marker end -->

# EKS Blueprint Blue deployment

## Table of content

- [EKS Blueprint Blue deployment](#eks-blueprint-blue-deployment)
  - [Table of content](#table-of-content)
  - [Folder overview](#folder-overview)
- [Terraform Doc](#terraform-doc)
  - [Requirements](#requirements)
  - [Providers](#providers)
  - [Modules](#modules)
  - [Resources](#resources)
  - [Inputs](#inputs)
  - [Outputs](#outputs)

## Folder overview

This folder contains Terraform code to deploy an EKS Blueprint configured to deploy workload with ArgoCD and associated workload repository.
This cluster will be used as part of our demo defined in [principal Readme](../README.md).

This deployment uses the local eks_cluster module. check it's [Readme](../modules/eks_cluster/README.md) to see what is include in this EKS cluster
