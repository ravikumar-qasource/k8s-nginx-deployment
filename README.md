# Nginx Kubernetes Deployment

This repository contains a Kubernetes manifest file for deploying Nginx with 5 replicas.

## Manifest Details

The `nginx-deployment.yaml` file defines the following configuration:

- **Deployment Name**: nginx-deployment
- **Replicas**: 5 instances
- **Image**: nginx:latest
- **Port**: 80
- **Update Strategy**: RollingUpdate
  - maxSurge: 1 (maximum number of pods that can be created above desired replicas)
  - maxUnavailable: 1 (maximum number of pods that can be unavailable during update)

### Resource Limits
- **CPU**: 
  - Request: 100m
  - Limit: 200m
- **Memory**:
  - Request: 128Mi
  - Limit: 256Mi

## Deployment Methods

### Method 1: Manual Deployment

1. Clone this repository:
   ```bash
   git clone https://github.com/ravikumar-qasource/k8s-nginx-deployment.git
   ```

2. Apply the manifest:
   ```bash
   kubectl apply -f nginx-deployment.yaml
   ```

3. Verify the deployment:
   ```bash
   kubectl get deployments
   kubectl get pods
   ```

### Method 2: Automated Deployment (GitHub Actions)

This repository includes a GitHub Actions workflow that automatically deploys the nginx manifest to your Kubernetes cluster whenever changes are pushed to the main branch.

#### Prerequisites for GitHub Actions:

1. Add your Kubernetes configuration as a base64-encoded secret in your GitHub repository:
   ```bash
   cat ~/.kube/config | base64 | pbcopy  # For macOS
   # OR
   cat ~/.kube/config | base64 | clip    # For Windows
   ```

2. In your GitHub repository:
   - Go to Settings > Secrets and Variables > Actions
   - Create a new secret named `KUBE_CONFIG`
   - Paste your base64-encoded kubeconfig as the value

The workflow will:
- Install kubectl
- Configure access to your cluster
- Deploy the manifest
- Verify the deployment status

## Scaling
The deployment is configured with 5 replicas by default. To scale the deployment:
```bash
kubectl scale deployment nginx-deployment --replicas=<desired_number>
```