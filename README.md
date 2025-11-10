
## Build Dockerfile
docker build -t ollama-llama3.2 .

## Run the Image
docker run -d -p 11434:11434 ollama-llama3.2
