### Phase 1: Environment Setup

### Create K8s v1.34 cluster (check if available)
```
kind create cluster --name ollama-k8s-v134 --image kindest/node:v1.34.0
```
<img width="2145" height="1155" alt="image" src="https://github.com/user-attachments/assets/72bfd0e4-9dd4-4241-8a10-bc87a0cba5b4" />

### Check if pods are running or not
```
kubectl get pods -A
```
### Deploy Ollama deployment for v1.34
```
kubectl apply -f ollama-v134-deployment.yaml
```
### Deploy service YAML file
```
kubectl apply -f ollama-v134-service.yaml
```
