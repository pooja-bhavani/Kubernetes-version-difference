# Kubernetes v1.33 vs v1.34 Performance Comparison
## AI Workload Optimization with Ollama

[![Kubernetes](https://img.shields.io/badge/Kubernetes-v1.33%20vs%20v1.34-blue)](https://kubernetes.io/)
[![Ollama](https://img.shields.io/badge/Ollama-AI%20Server-green)](https://ollama.ai/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)


## 🎯 Project Overview
This project provides a comprehensive comparison between Kubernetes v1.33 and v1.34, focusing on AI workload performance, specifically testing Ollama AI server with large language models. The goal is to provide concrete evidence for measurable upgrade in resource efficiency, cost optimization, and advanced features based on real-world testing with AI applications.

Test Application: Ollama AI Server with llama3.2:1b model (1.3GB)
Comparison Baseline: Docker deployment performance
Testing Methodology: Hands-on deployment and performance measurement

**Phase 1 Docker Foundation**

- Set up Ollama with Docker for local AI model deployment
- Test different LLM models and document performance
- Deployed Ollama with multiple AI models
- Tested performance across different model sizes
- Compared qwen2.5:0.5b vs llama3.2:1b vs tinyllama
- Understanding of LLM deployment basics

**Phase 2 : Kubernetes Migration**

- Deploy Ollama on Kubernetes v1.33 (kind cluster)
- Identify resource allocation challenges
- Deploy Ollama on Kubernetes v1.34 (kind cluster) 
- Demonstrating business value of upgrade
   
## 📋 Prerequisites

- Docker Desktop
- kubectl
- kind (Kubernetes in Docker)
- 8GB+ RAM, 4+ CPU cores

##  Quick Start

# Clone repository
```
git clone https://github.com/pooja-bhavani/Kubernetes-version-difference
```


### Phase 1: Docker Baseline Testing

# Pull and run Ollama container
```
docker pull ollama/ollama
docker run -d -p 11434:11434 --name ollama ollama/ollama
```
<img width="1402" height="235" alt="image" src="https://github.com/user-attachments/assets/11e47531-0611-428c-af76-9b42c61bcf39" />
<img width="1183" height="87" alt="image" src="https://github.com/user-attachments/assets/128d1b25-332d-4271-88cb-2681dd107d1f" />

### Download and test AI model
```
docker exec -it ollama ollama pull llama3.2:1b
docker exec -it ollama ollama run llama3.2:1b # 1.3GB 
```

<img width="1983" height="1415" alt="image" src="https://github.com/user-attachments/assets/97e52ef8-72df-4eed-9dff-5e73086bda84" />


*✅ Successfully running llama3.2:1b AI model on Docker* 
---

**Docker Results:**
- **Setup Time:** Fast (minutes)
- **Model Performance:** Responsive, smooth interaction
- **Resource Usage:** Stable, no crashes
- **User Experience:** Professional-grade performance
---

### 2. Different AI Models Pulls (Optional)

# Lightweight options (choose one)
```
docker exec -it ollama ollama pull qwen2.5:0.5b    # 394MB 
docker exec -it ollama ollama pull tinyllama       # 637MB 
```


## 📊 Model Comparison & Test Results

| Model | Size | Use Case | Performance | Response Quality |
|-------|------|----------|-------------|------------------|
| qwen2.5:0.5b | 394MB | Quick testing | Basic |Concise, accurate |
| tinyllama | 637MB | Development | Good | Simple, adds extra examples |
| llama3.2:1b | 1.3GB | Production | Better | Detailed, step-by-step |

# 🚀 Kubernetes Migration Steps

### Environment Setup

- **v1.33 Cluster:** kind cluster with ollama-v133 deployment
- **v1.34 Cluster:** kind cluster with ollama-v134 deployment  
- **Test Workload:** Ollama AI server with llama3.2:1b model (1.3GB)
- **Testing Period:** Real production simulation

### Phase 2: Kind Installation
```
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.23.0/kind-darwin-arm64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
```
```
kind version
```
## Repository Structure

```
├── v1.33-files/           # Alpha DRA implementation
│   ├── ollama-deployment-v1.33.yaml           # ollama testing
│   ├── ollama-service-v1.33.yaml
│   ├── dra
│   ├──dra-v1.33-crds.yaml                     # Required CRDs
│   ├── dra-v1.33-device-class.yaml            # v1alpha3 APIs
│   ├── dra-v1.33-gpu-workload.yaml            # 4-pod sharing
│   └── dra-v1.33-kind-cluster.yaml            # Feature gates required
│   ├── volumesAttributesClass
│   ├── volume-attributes-class-v133.yaml
├── v1.34-files/           # Stable DRA implementation  
│   ├── ollama-v134-deployment.yaml            # ollama testing
│   ├── ollama-v134-service.yaml
│   ├── dra.v1.34
│   ├── dra-v1.34-working.yaml                 # 8-pod demo (no GPU needed)
│   ├── dra-v1.34-gpu-workload.yaml            # REAL GPU: Requires actual hardware
│   ├── dra-v1.34-device-class.yaml            # REAL GPU: Requires NVIDIA plugin
│   └── pod-replacement-policy-v1.34.yaml      # Job improvements
│   ├── volumesAttributesClass
│   ├── volume-attributes-class-v1.34.yaml

```
## Key Differences Explained

### v1.33 (Alpha)
- **API**: `resource.k8s.io/v1alpha3`
- **Setup**: Requires custom CRDs (fake GPU simulation)
- **Sharing**: 4 pods per GPU (simulated)
- **Status**: Alpha (not production ready)

### v1.34 (Stable)  
- **API**: `resource.k8s.io/v1` (built-in)
- **Setup**: No CRDs needed (native support)
- **Sharing**: 8 pods per GPU (real or simulated)
- **Status**: Stable (production ready)
