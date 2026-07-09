---
title: "Summary: I Still Prefer MCP Over Skills"
type: summary
source_count: 1
created: 2026-06-22
last_updated: 2026-06-22
tags: [mcp, skills, ai-agents, architecture, developer-experience]
inbound_links: 0
status: complete
related_pages: ["[[concepts/model-context-protocol]]", "[[topics/ai-software-development]]"]
---

# Summary: I Still Prefer MCP Over Skills

**Source**: David, david.coffee, 2026-04-02
**URL**: https://david.coffee/i-still-prefer-mcp-over-skills/

---

## One-Paragraph Summary

The author argues against the growing narrative that "MCP is dead" and "Skills are the new standard." MCP should remain the standard for giving LLMs access to services (connectors), while Skills should focus on pure knowledge — teaching LLMs how to use existing tools, standardizing workflows, and capturing gotchas (manuals). Skills that require CLI installation are problematic due to deployment friction, secret management nightmares, fragmented ecosystems, and context bloat. The ideal pattern: a Skill as a knowledge layer on top of an MCP connector.

---

## Key Insights

- **MCP advantages over CLI-based Skills**: Zero-install remote usage, seamless updates, saner auth (OAuth), true portability (works from any client), natural sandboxing, smart discovery (tools loaded on demand)
- **Skills friction**: CLI installation requirements, plain-text secret management, fragmented ecosystem (different tools support different formats), entire SKILL.md loaded into context vs. single tool signature
- **The taxonomy**: MCP = **Connectors** (service access); Skills = **Manuals** (knowledge/context)
- **When to use MCP**: Any service integration (calendar, browser, databases, SaaS) — the service itself should dictate the interface
- **When to use Skills**: Teaching existing CLIs (curl, git, gh), standardizing workflows, capturing gotchas, business jargon, organizational context
- **Best pattern**: Skill as cheat sheet for the MCP — knowledge layer on top of connector layer; captures non-obvious patterns, date format quirks, truncation gotchas
- **Practical workflow**: After discovering MCP quirks in a session, ask Claude to package learnings into a Skill for future sessions
- **MCP Nest**: Author's product that tunnels local MCP servers through the cloud for remote accessibility

---

## Key Quote

> "It's like forcing someone to read the entire car's owner's manual when all they want to do is call `car.turn_on()`."

---

## Relevance to Wiki

- Adds the MCP-vs-Skills architectural debate to [[concepts/model-context-protocol]]
- Practical complement to the more theoretical/historical treatment in the existing MCP page
- The "connector + manual" mental model is a useful framework for agent infrastructure design

---

## Source Metadata

| Field | Value |
|---|---|
| Author | David (david.coffee) |
| Published | 2026-04-02 |
| Type | Blog post / opinion |
| Clipped | 2026-04-20 |
