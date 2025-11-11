# Kubernetes v1.34 vs v1.33 

## 🎯 Project Objective

**Phase 1 Docker Foundation**

- Set up Ollama with Docker for local AI model deployment
- Test different LLM models and document performance
- Deployed Ollama with multiple AI models
- Tested performance across different model sizes
- Compared qwen2.5:0.5b vs llama3.2:1b vs tinyllama

**Phase 2 :** Kubernetes Migration

- Deploy Ollama on Kubernetes v1.33 (kind cluster)
- Identify resource allocation challenges
- Research Kubernetes v1.34 dynamic resource benefits
- Create POC demonstrating business value of upgrade

## Prerequisites
- Docker installed and running
- Minimum 4GB RAM available
- Internet connection for model downloads

## 🚀 Quick Start

### 1. Pull and Run Ollama Container
```bash
docker pull ollama/ollama
docker run -d -p 11434:11434 --name ollama ollama/ollama
```
![alt text](image.png)

![alt text](image-9.png)

### 2. To Pull Multiple AI Models (optional)
```bash
# Lightweight options 
docker exec -it ollama ollama pull qwen2.5:0.5b    # 394MB 
docker exec -it ollama ollama pull tinyllama       # 637MB 
docker exec -it ollama ollama pull llama3.2:1b     # 1.3GB 
```
![alt text](image-8.png)

