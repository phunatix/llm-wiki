---
title: Model Context Protocol (MCP)
type: concept
source_count: 5
created: 2026-04-10
last_updated: 2026-06-22
tags: [mcp, ai-agents, protocols, governance, interoperability]
inbound_links: 0
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

From a platform engineering perspective, MCP servers are a new category of platform capability to expose, govern, and maintain. [[concepts/agentic-infrastructure]] describes the broader shift of AI agents becoming first-class platform actors; MCP is the protocol layer that makes this possible at scale. [[concepts/governance-by-default]] is the design pattern that should govern how MCP tools are exposed.

---

## MCP as Universal Plugin System

Beyond AI, MCP is accidentally becoming a **universal plugin system** — analogous to how USB-C transcended its original purpose. (Werner, 2025)

The insight: every MCP server built for AI becomes a free plugin for *any* application that speaks the protocol. A Spotify MCP built for Claude is instantly usable by a workout app, a task manager, or anything else — without the MCP developer knowing those apps exist.

**Protocol evolution precedent**: HTTP (academic papers → civilization), Bluetooth (hands-free → smart locks), USB (keyboards → power delivery). Great protocols always transcend their creators' intent. MCP isn't saying "I'm for AI" — it's saying "I'm a well-designed hole for functionality."

This creates an **accidental network effect**: more AI-driven MCP servers → more capabilities available to all apps → more incentive to speak MCP → more servers built. The flywheel accelerates regardless of whether participants are building for AI specifically.

---

## MCP vs. Skills: The Architecture Debate

A growing narrative claims "MCP is dead; Skills are the new standard." Practitioners push back with a clear taxonomy (david.coffee, 2026):

- **MCP = Connectors**: The standard for giving LLMs (or any app) an interface to services. The service dictates the interface. Advantages: zero-install remote usage, seamless updates, OAuth-based auth, natural sandboxing, smart discovery.

- **Skills = Manuals**: Pure knowledge that teaches LLMs *how to use* existing tools. Best for: standardizing workflows, capturing gotchas, teaching CLI usage patterns, encoding business jargon.

**Skills that require CLI installation are problematic**:
- Deployment friction (binaries, NPM, uv)
- Secret management nightmare (plain-text tokens in .env)
- Fragmented ecosystem (different clients support different formats)
- Context bloat (entire SKILL.md loaded vs. single tool signature)

**The ideal pattern**: A Skill as a **knowledge layer on top of an MCP connector** — the MCP handles connection and tool execution; the Skill captures non-obvious patterns, format quirks, and best practices discovered through use.

---

## Open Questions

- Which operational controls are most important to implement first: RBAC, budget caps, audit logging, or environment isolation?
- Will MCP standardize enough to become commodity, or will vendor-specific extensions fragment the ecosystem?
- How does MCP interact with existing API gateway and service mesh infrastructure?
- SDK code mode (where agents write and execute integration code using idiomatic SDKs) may outperform direct tool use for complex API tasks — how does this change the architecture of MCP-based agents?
- Will MCP's universal plugin potential be realized beyond AI, or will it remain primarily an AI-agent protocol?
- How does the Skill-as-knowledge-layer pattern scale in large organizations with hundreds of MCP servers?

---

## Sources

- [[sources/linux-foundation-google-anthropic-wer-den-standard-fuer-ki-agenten-setzt]] — Strategic context; Linux Foundation + Google + Anthropic backing; governance of the standard
- [[sources/managing-mcp-servers-and-tools-with-agentregistry-oss]] — Registry-oriented governance; AgentRegistry OSS; tool access controls
- [[summaries/mcp-is-eating-the-world--summary]] — Historical predecessors; four-good-enoughs framework; adoption flywheel; "designing at the right altitude" (Stainless, 2025)
- [[summaries/mcp-universal-plugin-system--summary]] — USB-C analogy; accidental network effect; protocol evolution precedents; MCP as possibility space beyond AI (Scott Werner, 2025)
- [[summaries/mcp-over-skills--summary]] — MCP vs Skills debate; connector/manual taxonomy; CLI-skill friction; knowledge layer pattern (david.coffee, 2026)
