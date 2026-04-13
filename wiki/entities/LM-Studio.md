---
title: LM Studio
type: entity
source_count: 1
created: 2026-04-13
last_updated: 2026-04-13
tags: [local-llm, ai-tools, self-hosted, developer-tools]
inbound_links: 0
status: complete
related_pages: ["[[topics/ai-software-development]]", "[[summaries/self-hosted-ai-coding--summary]]", "[[concepts/agentic-coding-risks]]"]
---

# LM Studio

**Category**: Software Tool (Local LLM Management / Serving)

**Quick Summary**: GUI tool for downloading, configuring, and serving local LLM models via an OpenAI-compatible API; enables self-hosted AI coding workflows without Docker or Python environments.

## Overview

LM Studio provides a user-friendly desktop interface for running LLMs locally. It handles model downloading, hardware-aware configuration (VRAM, context length, quantization), and serves models via a local OpenAI-compatible API. This makes it straightforward to build local AI coding setups connecting to tools like Roo Code in VS Code.

## Key Capabilities

- Model discovery and download (from Hugging Face)
- GPU/CPU offload configuration
- Flash Attention, KV caching options
- Local API server (port 1234, OpenAI-compatible)
- MCP server plugin support (for tool use in chat window)
- Support for GGUF quantized models

## Self-Hosted AI Coding Stack

```
LM Studio (serves models via local API)
├── Coder LLM: Qwen3-Coder-30B (GGUF quantized)
├── Embedding Model: Qwen3-Embedding-0.6B
└── MCP Plugin: docs-mcp-server (RAG over docs)
         ↑
VS Code + Roo Code (connects to LM Studio API)
         └── MCP Config pointing to docs-mcp-server
```

## Key Notes

- Qwen3 models: disable QV Caching (causes errors); use f16 default
- `DOCS_MCP_EMBEDDING_MODEL` must match the API Model Name shown in Server tab
- MCP servers in LM Studio only work in the chat window — Roo Code needs its own MCP config
- 20-35 T/s typical speed on consumer hardware (RTX 4070 Ti class)
- Advantages: 100% local/private, VRAM-friendly with quantized GGUF models

## Alternatives

- llama.cpp (CLI, faster but requires setup)
- Ollama (simpler API, less configuration control)
- Direct cloud APIs (not private, not local)

## See Also

- [[topics/ai-software-development]]
- [[summaries/self-hosted-ai-coding--summary]]
- [[concepts/agentic-coding-risks]]: Why local/private matters

## Sources

- [[summaries/self-hosted-ai-coding--summary]]: Full setup guide
