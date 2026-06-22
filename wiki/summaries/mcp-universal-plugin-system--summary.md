---
title: "Summary: MCP — An (Accidentally) Universal Plugin System"
type: summary
source_count: 1
created: 2026-06-22
last_updated: 2026-06-22
tags: [mcp, protocols, network-effects, plugin-systems, architecture]
inbound_links: 0
status: complete
related_pages: ["[[concepts/model-context-protocol]]", "[[topics/ai-software-development]]"]
---

# Summary: MCP — An (Accidentally) Universal Plugin System

**Source**: Scott Werner, worksonmymachine.ai, 2025-06-28
**URL**: https://worksonmymachine.ai/p/mcp-an-accidentally-universal-plugin

---

## One-Paragraph Summary

Werner argues that MCP's real power extends far beyond AI — it's accidentally becoming a universal plugin system, analogous to how USB-C became a universal connector beyond its original purpose. Every MCP server built for AI (Claude, ChatGPT) becomes a free plugin for *any* application that speaks the protocol, creating an unplanned network effect. The key insight: MCP isn't saying "I'm for AI" — it's saying "I'm a well-designed hole. Put something here." This mirrors historical protocol evolution where great protocols always get used for purposes their creators never imagined.

---

## Key Insights

- **The USB-C analogy**: MCP is a "possibility space" — not defined by what it's for, but by what it enables; like USB-C carrying power, data, video, and (apparently) toaster control
- **Accidental network effect**: Someone builds a Spotify MCP for AI → your workout app can now generate playlists → you wrote zero Spotify code → the MCP developer doesn't know your app exists → everyone wins
- **Protocol evolution precedent**: HTTP (academic papers → civilization), Bluetooth (hands-free → smart locks), USB (keyboards → emotional support fans) — great protocols always transcend original intent
- **The "Cigarette Lighter Principle"**: Protocols don't judge your use case; they provide a standardized interface and let users figure out what to plug in
- **"Remove the AI part"**: MCP docs say "standardized way to connect AI models to data sources and tools" — remove "AI models" and it's "standardized way to connect literally anything to data sources and tools"
- **APM (Actions Per Minute)**: Author's task management app uses MCP servers as its entire plugin system — spell check, coffee ordering, Warcraft peon responses — all just MCP servers

---

## Key Quote

> "MCP thinks it's for giving context to AI models. But really? It's just a really good protocol for making things talk to other things."

---

## Relevance to Wiki

- Adds the "universal plugin system" perspective to [[concepts/model-context-protocol]] — beyond governance and AI-specific framing
- The network effect argument strengthens the adoption flywheel analysis from the Stainless article
- Protocol evolution precedents provide historical grounding for MCP's trajectory

---

## Source Metadata

| Field | Value |
|---|---|
| Author | Scott Werner |
| Published | 2025-06-28 |
| Type | Newsletter / essay |
| Clipped | 2026-04-20 |
