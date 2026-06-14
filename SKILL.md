---
name: llm-deploy-helper
description: One-command LLM deployment — detect hardware (GPU/CPU/RAM), recommend optimal engine (vLLM/Ollama/llama.cpp), generate Docker Compose and systemd configs. Stop guessing which engine fits your machine.
version: 1.2.0
author: minirr890112-byte
license: MIT
metadata:
  hermes:
    tags: [LLM, Deployment, Docker, GPU, vLLM, Ollama, llama.cpp, DevOps]
    homepage: https://github.com/minirr890112-byte/llm-deploy-helper
---

# llm-deploy-helper

## Problem → Solution

**The problem**: You have a GPU. You want to run an LLM locally. Should you use vLLM? Ollama? llama.cpp? What model size fits your VRAM? How do you write the Docker Compose file? Three hours of blog posts later, you're still not sure.

**The solution**: One command detects your hardware (GPU model, VRAM, RAM, CPU cores, CUDA version) and recommends the optimal engine with scored reasoning. Then it generates a ready-to-use Docker Compose or systemd config. From hardware to running model in under 2 minutes.

## Quick Start

```bash
pip install git+https://github.com/minirr890112-byte/llm-deploy-helper.git

llm-deploy-helper check
llm-deploy-helper generate --engine ollama --model llama3.1:8b
llm-deploy-helper generate --engine vllm --model meta-llama/Llama-3.1-8B
llm-deploy-helper generate --engine llama.cpp --model llama3.1-8b-Q4_K_M.gguf
```

## Real Output

```
$ llm-deploy-helper check

╭────────────── System Information ──────────────╮
│ CPU Cores: 16      RAM: 64 GB                   │
│ GPU: RTX 4090      VRAM: 24 GB   CUDA: 12.4    │
╰─────────────────────────────────────────────────╯

╭────── Recommended Engines ──────╮
│ ⭐ vLLM       Score: 10/10      │
│    Best for 24 GB VRAM GPU      │
│ ⭐ Ollama     Score: 8/10       │
│    Easy setup, good GPU support │
│ ⭐ llama.cpp  Score: 9/10       │
│    CPU fallback, 64 GB RAM      │
╰─────────────────────────────────╯

$ llm-deploy-helper generate --engine ollama --model llama3.1:8b
✅ Generated docker-compose.yml
   GPU support: enabled (RTX 4090)
   Port: 11434
   Run: docker compose up -d
```

---
⭐ **Star this repo if you deployed an LLM without reading 10 blog posts**: [github.com/minirr890112-byte/llm-deploy-helper](https://github.com/minirr890112-byte/llm-deploy-helper)
