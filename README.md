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


## Table of Contents
1. [Pre-Migration Assessment](#pre-migration-assessment)
2. [Environment Setup](#environment-setup)
3. [DRA Implementation](#dra-implementation)
4. [PodReplacementPolicy Configuration](#podreplacement-policy-configuration)
5. [Pod-level Resources Deployment](#pod-level-resources-deployment)
6. [Testing & Validation](#testing--validation)
7. [Production Rollout](#production-rollout)
8. [Troubleshooting Guide](#troubleshooting-guide)

   
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
## Cluster Creation

### Create K8s v1.33 cluster (check if available)
```
kind create cluster --name ollama-k8s --image kindest/node:v1.33.0
```

### To display cluster information for  Kubernetes context
```
kubectl cluster-info --context kind-ollama-k8s
```
<img width="1644" height="506" alt="image" src="https://github.com/user-attachments/assets/b12c99d5-85cd-4088-a912-c2d007e5700c" />
<img width="1725" height="678" alt="image" src="https://github.com/user-attachments/assets/7f162a28-3bbb-4bb4-a7b0-a3e317498b15" />

