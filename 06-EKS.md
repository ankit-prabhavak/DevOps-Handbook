# Amazon EKS (Elastic Kubernetes Service) for DevOps

## Authentication & Cluster Connectivity

Generate or update your local kubeconfig file to authenticate against a specific EKS cluster:
```bash
aws eks update-kubeconfig --region ap-south-1 --name cluster-name
```

Verify cluster connection by retrieving the current status of the managed worker nodes:
```bash
kubectl get nodes
```

List all active EKS clusters managed by AWS in the configured region:
```bash
aws eks list-clusters --region ap-south-1
```

Describe structural configuration details of a specific EKS cluster control plane:
```bash
aws eks describe-cluster --name cluster-name --region ap-south-1
```

## Cluster Administration via eksctl CLI

Print the installed version of the eksctl CLI tool:
```bash
eksctl version
```

List all active EKS clusters managed by eksctl in the configured region:
```bash
eksctl get cluster
```

Spin up a new production-ready EKS cluster with default node configurations:
```bash
eksctl create cluster --name dev-cluster --nodes 2 --region ap-south-1
```

Tear down and completely remove an EKS cluster along with its underlying CloudFormation stacks:
```bash
eksctl delete cluster --name dev-cluster --region ap-south-1
```

## Node Group Management

List all EC2 worker node groups attached to a specific EKS cluster:
```bash
eksctl get nodegroup --cluster dev-cluster
```

Scale the capacity of an existing managed node group dynamically:
```bash
eksctl scale nodegroup --cluster=dev-cluster --name=standard-workers --nodes=4 --nodes-min=2 --nodes-max=6
```

Upgrade the underlying Amazon Machine Image (AMI) version of a managed node group:
```bash
eksctl upgrade nodegroup --name=standard-workers --cluster=dev-cluster --kubernetes-version=1.31
```

## IAM Roles for Service Accounts (IRSA) & Add-ons

Create an IAM OpenID Connect (OIDC) provider for the cluster to enable fine-grained pod permissions:
```bash
eksctl utils associate-iam-oidc-provider --cluster dev-cluster --approve
```

Create an IAM service account mapping a native Kubernetes service account to an AWS IAM role:
```bash
eksctl create iamserviceaccount --name cluster-autoscaler --namespace kube-system --cluster dev-cluster --attach-policy-arn arn:aws:iam::aws:policy/AutoScalingFullAccess --approve
```

List all installed EKS managed add-ons (such as VPC-CNI, CoreDNS, or Kube-Proxy):
```bash
aws eks list-addons --cluster-name cluster-name
```

## Cluster Troubleshooting & Logging

Query the live configuration state of control plane logging endpoints:
```bash
aws eks describe-cluster --name cluster-name --query "cluster.logging.clusterLogging"
```

Enable specific control plane log streams (API Server, Audit, Authenticator) to CloudWatch Logs:
```bash
aws eks update-cluster-config --name cluster-name --logging '{"clusterLogging":[{"types":["api","audit","authenticator"],"enabled":true}]}'
```
