<!-- note marker start -->
NOTE: This repo contains only the documentation for the private BoltsOps repo code.
Original file: https://github.com/boltops-pro/terraspace-pro-eks/blob/master/vendor/modules/eks/test/README.md
The docs are publish so they are available for interested subscribers.
For access to the source code, you can become a BoltOps subscriber.
See: https://learn.boltops.com

<!-- note marker end -->

# Terratest for EKS Blueprints

## Configure and run Terratest

The following steps can be used to configure Go lang and run Terratests locally(Mac/Windows machine)).

### Step 1: Install

[golang](https://go.dev/doc/install) (for macos you can use brew)

### Step 2: Change directory into the test folder.

```sh
cd test
```

### Step 3: Initialize your test

```sh
go mod init github.com/aws-ia/terraform-aws-eks-blueprints

go mod tidy -go=1.17
```

### Step 4: Build and Run E2E Test

```sh
cd src

go get -v -t -d && go mod tidy -compat=1.17

go test -v -timeout 60m -tags=e2e
```
