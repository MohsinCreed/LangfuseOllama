# Langfuse + Ollama (Local LLM Evaluation Setup)

This repository provides a local, free, self-hosted setup for
LLM evaluation using Langfuse and Ollama.

The goal is to:

- Experiment with prompts
- Compare multiple LLMs
- Run evaluations (scores, LLM-as-judge, datasets)
- Keep everything local and offline

This setup uses the official Langfuse OSS (version v3.148.0)
with a local Ollama instance via the OpenAI-compatible API.

No Langfuse code changes, forks, or plugins are required.

This follows the recommended integration approach documented in:
https://github.com/langfuse/langfuse

---

## PREREQUISITES

- Docker Desktop (WSL2 enabled on Windows)
- 16 GB RAM recommended
- Optional: NVIDIA GPU (for faster inference)

---

## STARTING THE STACK

From the project root directory, run:

docker compose up -d

This starts:

- Langfuse (UI + workers)
- PostgreSQL, ClickHouse, Redis, MinIO
- Ollama (CPU-only by default)

> **Tip:** the `docker-compose.yml` file includes an `ollama` service by default. If you already
> have Ollama installed natively on your PC and want to use that instead, simply **comment out**
> the `ollama` service block in `docker-compose.yml` (see example further below) and make sure
> your native Ollama is running and listening on port `11434`. Only one instance may bind to the
> port at a time.

---

## ACCESS LANGFUSE

Open your browser:

http://localhost:3000

First-time setup:

1. Create a user
2. Create an organization
3. Create a project

All Langfuse data is stored locally in Docker volumes.

---

## OLLAMA (LOCAL LLM RUNTIME)

Ollama runs inside Docker and exposes an OpenAI-compatible API.

If you're using the container, other services (like Langfuse) can reach it via the hostname
`http://ollama:11434/v1`. When using a native installation, point at
`http://host.docker.internal:11434/v1` instead and make sure the Docker service is commented out or stopped.

You can interact with Ollama in TWO ways:

1. Simple host command (recommended for most users)
2. Explicit Docker command (useful if you also have native Ollama)

Both are shown below.

---

## LIST AVAILABLE MODELS

Simple command:
ollama list

Docker-specific command:
docker exec -it ollama ollama list

NOTE:

- If you have native Ollama installed AND Docker Ollama running,
  the docker command guarantees you are talking to the container.

---

## PULL A MODEL (EXAMPLES)

Recommended models for evaluation:

Gemma 3 (4B) – primary eval / judge:
docker exec -it ollama ollama pull gemma3:4b

Mistral 7B – comparison model:
docker exec -it ollama ollama pull mistral

LLaMA 3.2 (3B) – reasoning comparison:
docker exec -it ollama ollama pull llama3.2:3b

After pulling, verify:

ollama list
or
docker exec -it ollama ollama list

---

## CONNECT OLLAMA TO LANGFUSE (UI)

In Langfuse UI:

Settings → LLM Connections → Add LLM Connection

Fill in exactly:

LLM adapter:
openai

Provider name:
OpenAI

API Key:
ollama

API Base URL:
http://ollama:11434/v1

> **Alternative:** if you run into networking issues from within containers, use
> `http://host.docker.internal:11434/v1` which resolves back to your host.  
> _(use `http://localhost:11434/v1` when pointing Langfuse at a native Ollama install.)_

Custom models:
Add model name as in Ollama: For example, gemma3:1b

Save the connection.

You can now select Ollama models in:

- Prompt Playground
- Evaluations
- Datasets
- LLM-as-Judge

NOTE

- Ollama must be running and reachable from Langfuse
- The model must already be pulled in Ollama
- Model names must match exactly (case-sensitive)
- This works for both CPU-only and GPU-enabled Ollama
- No external scripts or SDKs are required for UI usage

---

## PROMPT PLAYGROUND TRACING

By default, Prompt Playground runs are NOT traced.

To enable tracing:

1. Go to Settings → Tracing
2. Enable "Trace Prompt Playground runs"
3. Save

This allows:

- Viewing traces
- Running evaluations
- Adding runs to datasets

---

## OPTIONAL: ENABLE GPU SUPPORT (NVIDIA ONLY)

GPU support is DISABLED by default.

Requirements:

- NVIDIA GPU
- Latest NVIDIA drivers
- Docker Desktop (WSL2)
- NVIDIA Container Toolkit installed

Steps:

1. Open docker-compose.yml
2. Find the ollama service
3. Uncomment the GPU block
4. Restart Docker services:

docker compose down
docker compose up -d

---

## VERIFY GPU USAGE

Run:

docker exec -it ollama ollama ps

If GPU is enabled, GPU-related information will appear.
If running on CPU, this command still works but shows CPU usage.

---

## IMPORTANT NOTES

- CPU-only mode is sufficient for learning and evaluations
- GPU is recommended for larger models (7B+)
- Models are NOT auto-downloaded
- Each user chooses which models to pull
- No prompts or data leave your machine

---

## REPOSITORY PHILOSOPHY

- Infrastructure is versioned in Git
- Runtime data and models are local
- No secrets are committed
- Users have freedom to experiment
- This is a learning & evaluation environment, not production

---

## COMPATIBILITY

- Langfuse OSS: v3.148.0
- Ollama: OpenAI-compatible API
- Deployment: Local Docker
- Licensing: Fully open source

---

## END
