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
- An **ACM certificate** for HTTPS (if SSL is enabled, AWS SSL ARN).

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

## Example Usage
A complete example of using this Helm chart with custom values:
```sh
helm upgrade --install my-release amitsdalal/HelmIngressKit \
  --namespace $KUBE_NAMESPACE \
  --set image.repository=$REGISTRY \
  --set image.tag=$IMAGE_TAG \
  --set ingress.host=$DOMAIN_NAME \
  --set ingress.annotations.alb\.ingress\.kubernetes\.io/certificate-arn=$SSL_CERT_ARN
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

### How to Contribute
1. Fork the repository.
2. Create a feature branch.
3. Commit your changes.
4. Open a pull request with detailed information about your changes.

For issues or feature requests, please [open an issue](https://github.com/amitsdalal/HelmIngressKit/issues).
