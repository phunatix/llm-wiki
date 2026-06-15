---
title: "Summary: MCP — An (Accidentally) Universal Plugin System"
type: summary
source_count: 1
created: 2026-06-15
last_updated: 2026-06-15
tags: [summary, mcp, protocols, network-effects]
source_file: "raw/inbox/MCP An (Accidentally) Universal Plugin System.md"
related_pages:
  - concepts/model-context-protocol
  - topics/ai-software-development
status: complete
---

# Summary: MCP — An (Accidentally) Universal Plugin System

**Source**: worksonmymachine.ai — "MCP: An (Accidentally) Universal Plugin System"
**Author**: Scott Werner
**URL**: https://worksonmymachine.ai/p/mcp-an-accidentally-universal-plugin
**Published**: 2025-06-28 | **Clipped**: 2026-04-10
**Type**: Opinion / conceptual essay

---

## Key Takeaways

**The USB-C analogy**: USB-C was designed for charging and data transfer. Because of how it's designed, it now carries video, display output, and apparently HDMI. The protocol doesn't judge your use case — it's a "possibility space." MCP is the same: designed to give AI context, but really a generic "standardized way to connect things to data sources and tools."

**The cigarette lighter principle**: Car cigarette lighters (now universal power outlets shaped like something from 1952) don't care what's plugged in. The protocol doesn't judge. MCP's tool interface doesn't care if it's being called by Claude or by a workout app or by a task management system.

**The accidental network effect**:
1. Someone builds an MCP server for their AI to access Spotify
2. Your workout app can now generate playlists
3. You didn't write any Spotify code
4. The Spotify MCP developer doesn't know your app exists
5. Everyone wins

Every MCP server built for AI becomes a free plugin for any application that speaks MCP. The ecosystem builds without central coordination.

**Protocol evolution pattern**: HTTP was for papers → runs civilization. Bluetooth was for calls → unlocks doors. USB was for keyboards → charges everything. MCP thinks it's for giving AI context. It may become something much larger.

---

## Connections

- [[concepts/model-context-protocol]] — USB-C analogy and accidental network effect are core conceptual frames
