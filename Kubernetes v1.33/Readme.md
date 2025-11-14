
## Cluster Creation

## Simple Start (Recommended)
1. Create basic cluster for Ollama testing
2. Later recreate with DRA config for advanced features

### DRA Testing Options
[DRA-kind-cluster](dra-kind-cluster.yaml)

### Create K8s v1.33 cluster (check if available)
```
kind create cluster --name ollama-k8s --image kindest/node:v1.33.0
```

### To display cluster information for  Kubernetes context
```
kubectl cluster-info --context kind-ollama-k8s
```

<img width="1644" height="506" alt="image" src="https://github.com/user-attachments/assets/842d7234-3075-4075-9caa-41a730105218" />
<img width="1725" height="678" alt="image" src="https://github.com/user-attachments/assets/13599c1c-118e-4237-a3bd-9f750b5f066d" />

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

## 🔬 Advanced Feature Testing: Dynamic Resource Allocation (DRA)

### Why Test DRA?
- **Problem**: Traditional GPU allocation wastes 70-90% capacity
- **Solution**: DRA enables GPU sharing for AI workloads like Ollama
- **Business Impact**: 87.5% cost reduction potential

### Install Custom Resource Definitions 
[dra-v133-crds.yaml](dra-v133-crds.yaml)
```
kubectl apply -f v1.33-files/dra-v133-crds.yaml
```
<img width="1409" height="228" alt="image" src="https://github.com/user-attachments/assets/7eed0445-c527-4df0-8844-e1f89201fd44" />

### Verify DRA APIs are available
```
kubectl api-resources | grep -E "(deviceclass|resourceclaim)"
```
## Create DeviceClass for GPU sharing
[dra-v133-device-class.yaml](dra-v133-device-class.yaml)
```
kubectl apply -f v1.33-files/dra-v133-device-class.yaml
```
## Create ResourceClaimTemplate

[dra-v133-gpu-workload.yaml](dra-v133-gpu-workload.yaml)
```
kubectl apply -f v1.33-files/dra-v133-gpu-workload.yaml
```






















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
