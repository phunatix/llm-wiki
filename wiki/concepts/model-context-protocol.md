---
title: Model Context Protocol (MCP)
type: concept
source_count: 3
created: 2026-06-15
last_updated: 2026-06-15
tags:
  - concept
  - ai-tooling
  - protocols
  - mcp
related_pages:
  - topics/ai-software-development
  - concepts/agentic-development-loop
status: complete
---

# Model Context Protocol (MCP)

**Domain**: AI Tooling / Protocols / Agent Infrastructure

**One-line definition**: An open, vendor-neutral protocol that standardizes how AI agents connect to external tools and data sources — the "USB-C for AI" that enables any tool to work with any LLM client without custom wiring.

---

## Definition

Model Context Protocol (MCP) is an open standard (released by Anthropic, November 2024; exploded in adoption February 2025) that provides a shared interface for connecting LLM agents to tools, services, and data sources. Instead of each LLM provider requiring custom integration per tool, and each tool requiring separate connectors per LLM, MCP defines one protocol that any client and any server can speak.

**Core idea**: An MCP server exposes tools with well-defined schemas. Any MCP client (Claude, ChatGPT, Cursor, Zed, etc.) can discover and call those tools without knowing anything about the underlying service implementation.

---

## Why MCP Succeeded Where Others Failed

Previous attempts at LLM tool integration all had structural flaws:

| Predecessor | Problem |
|---|---|
| Function/tool calling | Manual per-request wiring; each provider had slightly different schemas |
| ReAct / LangChain | Model emits `Action:` strings; parse them yourself — fragile, hard to debug |
| ChatGPT plugins | Gated; required hosting an OpenAPI server + Anthropic approval |
| Custom GPTs | Locked inside OpenAI's runtime |
| AutoGPT / BabyAGI | Configuration mess; error cascades |

Stainless (2025) identifies four reasons MCP succeeded where these didn't:

1. **Models finally good enough**: Tool use in agentic settings requires robust error handling. Early models got sucked into error spirals ("context poisoning"). Newer models recover from mistakes. Once models cross the reliability threshold, tool integration overhead drops dramatically. "MCP just showed up right on time."

2. **Protocol is good enough**: Vendor-neutral. Define a tool once; it's accessible to any MCP-capable client. Clear separation between tool developer and agent developer — each can focus on their side. Designed "at the right altitude" — exposing the right amount of detail.

3. **Tooling is good enough**: Simple, high-quality SDKs in many languages. A Python MCP server is a decorated function + a runtime. Low friction to build, share, and reuse.

4. **Momentum is good enough**: OpenAI and Google adopted MCP. All major model providers are onboard. Rich ecosystem: registries (smithery.ai, glama.ai), services (Cloudflare, Vercel), courses (HuggingFace). As MCP becomes ubiquitous, models will be trained on MCP usage patterns, compounding capability.

---

## The Accidental Network Effect

Scott Werner's "USB-C analogy" captures the emergent property:

> "Every MCP server built for Claude or ChatGPT becomes a free plugin for *anything* that speaks MCP."

Protocol evolution pattern:
- HTTP was for academic papers → now runs civilization
- Bluetooth was for hands-free calling → now unlocks your front door
- USB was for keyboards → now charges everything

MCP was designed to give AI agents context. But because it's a generic "standardized way to connect things to data sources and tools," it's accidentally creating a **universal plugin ecosystem** — not just for AI.

---

## MCP vs. Skills: Connectors vs. Manuals

David (david.coffee, 2026) makes the clearest distinction:

**Use MCP when**: Giving an LLM an interface to *connect to something* — a website, a service, an application. MCP handles auth, sandboxing, updates, portability.

**Use Skills when**: Pure knowledge and context — teaching the LLM *how* to use tools it already has, standardizing workflows, capturing domain jargon.

**MCP advantages over Skills-with-CLI**:
- **Zero-install remote usage**: Point client at MCP URL, done
- **Seamless updates**: New tools instantly available to all clients
- **OAuth auth**: No raw tokens in plain text
- **True portability**: Works from any device, any client
- **Sandboxing**: Controlled interface, not raw execution power
- **Smart discovery**: Tools loaded on-demand, not pre-loaded into context

**Problems with Skills requiring CLI**:
- CLI must be installed — fails in non-terminal clients (ChatGPT, Perplexity web)
- Secret management nightmare (where do API tokens live?)
- Fragmented ecosystems and incompatible formats
- Context bloat: entire SKILL.md loaded even if only one tool is needed

**The ideal pattern**: MCP as connector + a companion Skill as the knowledge layer — the Skill captures gotchas, edge cases, and best practices discovered during use. The MCP handles the actual connection.

---

## Practical Architecture

A minimal MCP server (Python):

```python
from mcp.server.fastmcp import FastMCP

mcp = FastMCP("MyService")

@mcp.tool()
def get_data(query: str) -> str:
    """Fetch data for a given query."""
    ...
```

Start it: `mcp dev path.to.your.module`

That's it — the tools are now available to any MCP client.

---

## Current Limitations

- Compatibility between MCP clients varies (different JSON Schema dialects, feature sets)
- Auth standardization is still maturing
- Performance degrades with many tools loaded (context window pressure)
- The line between when to use a local vs. remote MCP server is still being worked out in practice

---

## Related Pages

- [[topics/ai-software-development]] — MCP is infrastructure for the agentic development ecosystem
- [[concepts/agentic-development-loop]] — MCP servers are part of the infrastructure Kakkar refers to

---

## Sources

- [[summaries/mcp-is-eating-the-world--summary]] — Stainless; four reasons MCP succeeded; momentum and ecosystem
- [[summaries/mcp-universal-plugin-summary]] — Scott Werner; USB-C analogy; accidental network effect
- [[summaries/mcp-vs-skills-summary]] — David (david.coffee); connectors vs manuals; MCP advantages; ideal combination pattern
