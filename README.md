# Kubernetes v1.34 vs v1.33 

## 🎯 Project Objective
**Phase 1 Docker Foundation**

- Set up Ollama with Docker for local AI model deployment
- Test different LLM models and document performance
- Deployed Ollama with multiple AI models
- Tested performance across different model sizes
- Compared qwen2.5:0.5b vs llama3.2:1b vs tinyllama
- Understanding of LLM deployment basics

**Phase 2 :** Kubernetes Migration

- Deploy Ollama on Kubernetes v1.33 (kind cluster)
- Identify resource allocation challenges
- Research Kubernetes v1.34 dynamic resource benefits
- Create POC demonstrating business value of upgrade

## Prerequisites
- Docker installation
- Kind (Kubernetes inside Docker)

##  Quick Start

### 1. Pull and Run Ollama Container
```bash
docker pull ollama/ollama
docker run -d -p 11434:11434 --name ollama ollama/ollama
```
<img width="1402" height="235" alt="image" src="https://github.com/user-attachments/assets/11e47531-0611-428c-af76-9b42c61bcf39" />


<img width="2541" height="865" alt="image" src="https://github.com/user-attachments/assets/d09c25c5-653f-4cea-be2b-a1d0616d161c" />



### 2. To Pull Multiple AI Models (optional)
```bash
# Lightweight options 
docker exec -it ollama ollama pull qwen2.5:0.5b    # 394MB 
docker exec -it ollama ollama pull tinyllama       # 637MB 
docker exec -it ollama ollama pull llama3.2:1b     # 1.3GB 
```
<img width="1359" height="145" alt="image" src="https://github.com/user-attachments/assets/0c17c295-8ae0-47ed-b2c8-6da38565ed5e" />

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
