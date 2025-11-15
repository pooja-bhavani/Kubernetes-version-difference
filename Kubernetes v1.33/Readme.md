## Cluster Creation

## Simple Start (Recommended)
1. Create basic cluster for Ollama testing
2. Later recreate with DRA config for advanced features

### DRA Testing Options
[DRA-kind-cluster](dra/dra-v133-kind-cluster.yaml)

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
[ollama-deployment-v1.33.yaml](ollama-deployment-v1.33.yaml)
```
kubectl apply -f ollama-deployment-v1.33.yaml   
```

### Apply service file
[ollama-service-v1.33.yaml](ollama-service-v1.33.yaml)
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
[dra-v133-crds.yaml](dra/v133-crds.yaml)
```
kubectl apply -f v1.33-files/dra-v133-crds.yaml
```
<img width="1409" height="228" alt="image" src="https://github.com/user-attachments/assets/b6662e28-f810-4980-84ac-a85e5f3bbefe" />

### Verify DRA APIs are available
```
kubectl api-resources | grep -E "(deviceclass|resourceclaim)"
```
<img width="1831" height="184" alt="image" src="https://github.com/user-attachments/assets/b22e53e0-87bc-4e2f-9b01-e1a37631b1e8" />

## Create DeviceClass for GPU sharing
[dra-v133-device-class.yaml](dra/v133-device-class.yaml)
```
kubectl apply -f v1.33-files/dra-v133-device-class.yaml
```
## Create ResourceClaimTemplate

[dra-v133-gpu-workload.yaml](dra/v133-gpu-workload.yaml)
```
kubectl apply -f v1.33-files/dra-v133-gpu-workload.yaml
```
<img width="1434" height="279" alt="image" src="https://github.com/user-attachments/assets/c063e734-c02e-484a-a97b-5d9595a050e8" />

#### 4 pods can share 1 GPU through time-slicing with 1-second intervals, instead of needing 4 separate GPUs.

### Check pods status
```
kubectl get pods -l app=ollama-dra-v133
```
<img width="1373" height="439" alt="image" src="https://github.com/user-attachments/assets/b8ea9b14-3948-4904-93ec-7a34d3703a90" />

---

### Test 1: Multi-container Resource Limitation
[multi-container-v133-per-container-resources.yaml](dra/multi-container-v133-per-container-resources.yaml)
```
kubectl apply -f multi-container-v133-per-container-resources.yaml
```
#### Demonstrates: Per-container allocation only, no sharing

<img width="1494" height="320" alt="image" src="https://github.com/user-attachments/assets/4e792d90-ab42-4eda-a53c-fc4217768f95" />

#### Demonstrates: Per-container allocation only, no sharing

---

### Test 2: Job Replacement Behavior
[pod-replacement-policy-v133.yaml](pod-replacement-policy-v133.yaml)

```
kubectl apply -f pod-replacement-policy-v133.yaml
```
#### Demonstrates: Immediate replacement, resource overlap

<img width="1489" height="575" alt="image" src="https://github.com/user-attachments/assets/6ff89a16-d519-44d6-b1b4-e98974cae0ee" />

---

### Test 3: DRA Alpha APIs

- Deploy Ollama with DRA configuration
[ollama-with-dra-v133.yaml](dra/ollama-with-dra-v133.yaml)
```
kubectl apply -f v1.33-files/ollama-with-dra-v133.yaml
```
#### Demonstrates: Alpha APIs, manual setup required

### Get pod name for DRA-enabled Ollama
```
POD_NAME=$(kubectl get pods -l app=ollama-dra-v133 -o jsonpath='{.items[0].metadata.name}')
```

### Test Ollama in DRA-enabled pod
```
kubectl exec -it $POD_NAME -- ollama pull llama3.2:1b
kubectl exec -it $POD_NAME -- ollama run llama3.2:1b
kubectl port-forward svc/ollama-dra-v133-service 11434:11434
```
<img width="1760" height="761" alt="image" src="https://github.com/user-attachments/assets/6d7af8fb-3767-43e5-897a-7f4ad22e5a8f" />
<img width="2932" height="733" alt="image" src="https://github.com/user-attachments/assets/a211bf88-d8ab-4d12-8b66-73386a76b2f9" />

---

### VolumeAttributesClass Test Result in v1.33
[VolumeAttributesClass.yaml](VolumeAttributesClass/volume-attributes-class-v133.yaml)

```
kubectl apply -f volume-attributes-class-v133.yaml
```
<img width="2283" height="465" alt="image" src="https://github.com/user-attachments/assets/93d455f9-d847-4b93-b11a-9ebfdad1e052" />

#### This proves v1.33 limitation:
- ❌ VolumeAttributesClass NOT SUPPORTED in v1.33
- ❌ No dynamic volume modification capability
- ❌ Static storage only - can't optimize costs

---

## v1.33 Pod-Level Resource Test

[restart-policy-global-v1.33.yaml](Pod-level-resources/restart-policy-global-v1.33.yaml)

```
kubectl apply -f restart-policy-global-v1.33.yaml
```
<img width="1726" height="397" alt="image" src="https://github.com/user-attachments/assets/b7a22fb7-8770-4522-95b8-0877a020988b" />
<img width="1724" height="1120" alt="image" src="https://github.com/user-attachments/assets/b8196082-dafd-4b31-acee-9cd44387d334" />
<img width="1559" height="818" alt="image" src="https://github.com/user-attachments/assets/95fa91f1-d7ae-4d3e-ba4c-7e47a10eab54" />

---

### container-restart-rules testing

[restart-policy-global-v1.33.yaml](container-restart-rules/restart-policy-global-v1.33.yaml)
```
kubectl apply -f restart-policy-global-v133.yaml
```
<img width="1573" height="650" alt="image" src="https://github.com/user-attachments/assets/df34d8e9-c0a2-497b-9ad3-b2f191f196d0" />

**v1.33: Global restart policy only causes all containers to restart together**

---

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
