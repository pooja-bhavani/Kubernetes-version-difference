### Phase 1: Environment Setup

# Create K8s v1.34 cluster (check if available)
```
kind create cluster --name ollama-k8s-v134 --image kindest/node:v1.34.0
```
# Deploy Ollama with Pod-level resources
```
kubectl apply -f ollama-v134-deployment.yaml
```
# Enable DRA features for GPU support
```
kubectl apply -f dra-device-class.yaml
```
