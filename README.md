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

## How to Deploy

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

## Scaling
The deployment is configured with 5 replicas by default. To scale the deployment:
```bash
kubectl scale deployment nginx-deployment --replicas=<desired_number>
```