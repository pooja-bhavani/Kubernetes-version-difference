FROM ollama/ollama:latest

RUN ollama serve & sleep 5 && ollama pull llama3.2:1b && pkill ollama

CMD ["ollama", "serve"]
