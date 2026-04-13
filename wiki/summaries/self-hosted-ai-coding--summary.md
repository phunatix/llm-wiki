---
title: "Self-Hosted AI Coding with LM Studio — Summary"
type: summary
source_count: 1
created: 2026-04-13
last_updated: 2026-04-13
tags: [ai, local-llm, self-hosted, developer-tools]
inbound_links: 0
status: complete
related_pages: ["[[entities/LM-Studio]]", "[[topics/ai-software-development]]"]
---

# Self-Hosted AI Coding with LM Studio — Summary

**Author**: u/xrailgun (Reddit r/LocalLLaMA)
**Source**: reddit.com/r/LocalLLaMA
**Date**: August 2025

## One-Paragraph Summary

A practical guide to setting up a fully local, private AI coding assistant using LM Studio (model serving), Qwen3-Coder (coding LLM), Qwen3-Embedding (for RAG), docs-mcp-server (documentation RAG via MCP), and VS Code + Roo Code (IDE/agent frontend). The stack avoids Docker, manages everything through GUIs, and runs entirely on consumer hardware (RTX 4070 Ti class).

## The Stack

| Component | Role |
|---|---|
| LM Studio | Download, configure, serve models via local OpenAI-compatible API |
| Qwen3-Coder-30B (GGUF) | Primary coding LLM |
| Qwen3-Embedding-0.6B | Embeddings for RAG |
| docs-mcp-server (arabold) | Scrapes and indexes docs; MCP server for RAG |
| VS Code + Roo Code | IDE with agent capabilities, connects to LM Studio |

## Key Steps

1. Install LM Studio → download Qwen3-Coder + Qwen3-Embedding models
2. Configure docs-mcp-server in LM Studio chat window (mcp.json)
3. Start local server in LM Studio (coder + embedding loaded)
4. Install Roo Code in VS Code → connect to LM Studio API
5. Configure Roo Code MCP to point to docs-mcp-server

## Important Notes

- Qwen3: disable QV Caching (causes exit code errors); use f16 default
- MCP in LM Studio only works in chat window — Roo Code needs its own MCP config
- `DOCS_MCP_EMBEDDING_MODEL` must match API Model Name in LM Studio Server tab
- GGUF format required (not MLX) for Flash Attention options
- ~20-35 T/s on RTX 4070 Ti hardware

## Filing Status

- [x] All sections complete
