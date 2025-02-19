# HelmIngressKit

HelmIngressKit is a Helm chart designed to deploy a Node.js (or any web-based) microservice on AWS EKS with an ALB (Application Load Balancer) ingress.

## Features
- Deploys a containerized web service to EKS.
- Configures AWS ALB ingress with SSL and health checks.
- Supports private image registries via `imagePullSecrets`.
- Fully customizable through `values.yaml`.

## Prerequisites
Before using this chart, ensure you have:
- Kubernetes cluster on **AWS EKS**.
- **Helm 3** installed.
- AWS Load Balancer Controller configured.
- An **ACM certificate** for HTTPS (if SSL is enabled, aws ssl arn).

## Installation
### 1. Add the Helm repository (if applicable)
```sh
helm repo add amitsdalal https://github.com/amitsdalal/HelmIngressKit.git
helm repo update
```

### 2. Install the chart
```sh
helm install my-release amitsdalal/HelmIngressKit -f values.yaml
```
Replace `my-release` with your preferred release name.

## Configuration
Modify the `values.yaml` file to customize the deployment. Below are key configurations:

### **Replica Count**
Set the number of instances for high availability:
```yaml
replicaCount: 2
```

### **Image Settings**
Define the container image and tag:
```yaml
image:
  repository: registry.gitlab.com/your-repo/eks-play
  tag: latest
```

### **Ingress Settings**
Configure ALB ingress for external access:
```yaml
ingress:
  enabled: true
  host: <your-domain>
  path: /graphql
  annotations:
    alb.ingress.kubernetes.io/scheme: "internet-facing"
    alb.ingress.kubernetes.io/certificate-arn: "<your-acm-arn>"
```

## Upgrade
To upgrade to a new version:
```sh
helm upgrade my-release amitsdalal/HelmIngressKit -f values.yaml
```

## Uninstall
To remove the deployment:
```sh
helm uninstall my-release
```

## License
This Helm chart is open-source and available under the MIT license.

## Contributing
Feel free to open issues or pull requests to improve HelmIngressKit!
