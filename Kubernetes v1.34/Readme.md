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
### Pull AI Model and run in K8s v1.34
```
kubectl exec -it ollama-v134-5c868b4dc4-z2qrw -- ollama pull llama3.2:1b
```
```
kubectl exec -it ollama-v134-5c868b4dc4-z2qrw -- ollama pull llama3.2:1b
```
<img width="1895" height="1079" alt="image" src="https://github.com/user-attachments/assets/f1cc729d-319f-441c-a1bb-0746e55f2200" />

# 🔬 Advanced Feature Testing: Dynamic Resource Allocation (DRA)

- v1.34 DRA uses stable APIs - no special cluster configuration needed
- No feature gates required - DRA is built-in
- Backward compatible - existing cluster can run v1.34 workloads











### Success Criteria for v1.34
- Inference Speed: 50%+ improvement
- Memory Efficiency: Dynamic allocation 2-4GB
- Reliability: Zero OOM kills
- Scalability: Support multiple models
