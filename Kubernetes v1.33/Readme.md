# Kubernetes v1.33 Testing

### Apply Deployment file
```
kubectl apply -f ollama-deployment-v1.33.yaml   
```

### Apply service file
```
kubectl apply -f ollama-service-v1.33.yaml
```

### Check Pods status
```
kubectl get pods
```

## Pull AI Model and run in K8s v1.33
```
kubectl exec -it <pod name> -- ollama pull llama3.2:1b 
```
```
kubectl exec -it <pod name> -- ollama run llama3.2:1b 
```
<img width="2161" height="738" alt="image" src="https://github.com/user-attachments/assets/3be0d8d6-5a9f-4040-b6bb-511f07390fcb" />

---

## Cluster Creation

## Option A: Simple Start (Recommended)
1. Create basic cluster for Ollama testing
2. Later recreate with DRA config for advanced features

### Create K8s v1.33 cluster (check if available)
```
kind create cluster --name ollama-k8s --image kindest/node:v1.33.0
```

### To display cluster information for  Kubernetes context
```
kubectl cluster-info --context kind-ollama-k8s
```
# DRA Testing Options
[DRA-kind-cluster](DRA-kind-cluster.yaml)





































### Kubernetes v1.33
**Advantages:**
- Container orchestration capabilities
- Service discovery and networking
- Declarative configuration management
- Built-in monitoring and logging integration

**Disadvantages:**
- **Critical:** Very slow AI inference performance
- **Critical:** OOM kills with large models (Exit 137)
- Fixed resource allocation causes waste
- Long deployment times (19+ minutes)
- Cannot run multiple AI models simultaneously
- Poor user experience for AI applications

---
