FROM ollama/ollama:latest

RUN apt update && apt install -y curl && \
    curl -fsSL https://claude.ai/install.sh | su - ubuntu -c 'bash'

RUN apt install -y python3-venv python3-pip wget git

USER ubuntu

WORKDIR /workspace
