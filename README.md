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

### 1. Ollama Containerization
```bash
docker pull ollama/ollama
docker run -d -p 11434:11434 --name ollama ollama/ollama
```
<img width="1402" height="235" alt="image" src="https://github.com/user-attachments/assets/11e47531-0611-428c-af76-9b42c61bcf39" />
<img width="1183" height="87" alt="image" src="https://github.com/user-attachments/assets/128d1b25-332d-4271-88cb-2681dd107d1f" />


### 2. Testing LLM on Docker

#### You can Pull Multiple smaller AI Models for Performance Comparison (optional)
```bash
# Lightweight options 
docker exec -it ollama ollama pull qwen2.5:0.5b    # 394MB 
docker exec -it ollama ollama pull tinyllama       # 637MB 
```
<img width="1359" height="145" alt="image" src="https://github.com/user-attachments/assets/c611036b-dad4-4f72-8d0c-33725edd896f" />



### 3. Production Model Testing - llama3.2:1b inside Docker Container
```bash
docker exec -it ollama ollama pull llama3.2:1b 
docker exec -it ollama ollama run llama3.2:1b # 1.3GB 
```
<img width="1908" height="310" alt="image" src="https://github.com/user-attachments/assets/f6c73f7c-5599-4c42-a33d-b68d86504c5e" />

<img width="2539" height="787" alt="image" src="https://github.com/user-attachments/assets/02564008-1480-4b0e-b0e2-4109c84cfd2a" />

*llama3.2:1b AI model running successfully on Docker - baseline for Kubernetes comparison*
---


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


