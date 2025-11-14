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

### Step 1: Check current cluster
```
kind get clusters
```
### Switching to the existing k8s-v134 cluster context
```
kubectl config use-context kind-k8s-v134
```
### # Deploy DeviceClass and ResourceClaimTemplate (stable v1 APIs)
[dra-v1.34-device-class.yaml](dra.v1.34/dra-v1.34-device-class.yaml)
```
kubectl apply -f dra-v1.34-device-class.yaml 
```
# Deploy the 8-pod GPU sharing workload
[dra-v1.34-gpu-workload.yaml](dra-v1.34-gpu-workload.yaml)
```
kubectl apply -f dra-v1.34-gpu-workload.yaml
```
<img width="2314" height="650" alt="image" src="https://github.com/user-attachments/assets/9a31b000-1ea7-48cd-9a0e-d59d5157d2e7" />







### Success Criteria for v1.34
- Inference Speed: 50%+ improvement
- Memory Efficiency: Dynamic allocation 2-4GB
- Reliability: Zero OOM kills
- Scalability: Support multiple models
