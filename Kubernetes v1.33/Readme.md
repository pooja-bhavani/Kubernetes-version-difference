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


### Problems Identified

#### 1. Deployment Performance Issues
- **Model downloads:** 19+ minutes (vs 3-10 min with Docker)
- **Image pulls:** Slow network optimization
- **Startup times:** Unacceptable for production scaling

#### 2. Memory Management Failures
- **OOM kills:** Exit code 137 when running llama3.2:1b
- **Multi-model conflicts:** Cannot run multiple AI models simultaneously
- **Fixed limits:** 2Gi insufficient for larger models (1.3GB + overhead)

#### 3. Inference Performance Degradation
- **Slow responses:** 3-5x slower than Docker deployment
- **Resource starvation:** CPU/memory constraints affect user experience
- **No GPU support:** Limited to CPU-only inference

#### 4. Operational Challenges
- **Resource planning:** Fixed allocation prevents optimization
- **Scaling limitations:** Cannot dynamically adjust to workload demands
- **Model management:** Poor handling of multiple AI models
