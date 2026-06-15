---
title: "Summary: I Still Prefer MCP Over Skills"
type: summary
source_count: 1
created: 2026-06-15
last_updated: 2026-06-15
tags: [summary, mcp, skills, ai-tooling, architecture]
source_file: "raw/inbox/I Still Prefer MCP Over Skills.md"
related_pages:
  - concepts/model-context-protocol
  - topics/ai-software-development
status: complete
---

# Summary: I Still Prefer MCP Over Skills

**Source**: david.coffee — "I Still Prefer MCP Over Skills"
**Author**: David
**URL**: https://david.coffee/i-still-prefer-mcp-over-skills/
**Published**: 2026-04-02 | **Clipped**: 2026-04-10
**Type**: Practitioner opinion / architectural argument

---

## Key Takeaways

**The emerging debate**: The AI space is pushing "Skills" (SKILL.md, slash commands, CLI wrappers) as the new standard for LLM capabilities. The author disagrees for service integration.

**MCP advantages for service connectivity**:
- Zero-install remote usage (just point at URL)
- Seamless updates (every client gets new tools instantly)
- Saner auth (OAuth, not raw tokens in .env files)
- True portability (works from Mac, phone, web, any MCP client)
- Sandboxing (controlled interface, not raw execution)
- Smart discovery (tools loaded on-demand, not pre-loaded into context)

**Problems with Skills requiring CLI**:
- Fails in non-terminal clients (ChatGPT, Perplexity web, standard Claude)
- Deployment mess (publish to npm/binaries, manage installation per environment)
- Secret management nightmare (tokens in plain text .env files; some ephemeral environments wipe secrets)
- Context bloat (entire SKILL.md loaded even for one tool call)
- Fragmented ecosystems (incompatible formats between Claude Code, Codex, Claude Cowork)

**The right model — Connectors vs. Manuals**:
- **MCP = Connector**: Standardized interface to a service; handles auth, execution, sandboxing
- **Skills = Manual**: Knowledge layer; teaches the LLM how to use tools, captures jargon, standardizes workflows
- **The ideal**: Skill as a knowledge layer *on top of* an MCP connector — captures gotchas, non-obvious patterns, and best practices discovered during use

**Practical pattern**: After discovering quirks in a NotePlan MCP session (date format must be YYYY-MM-DD, search truncates without a parameter bump), ask Claude to package everything learned into a Skill. The MCP handles connection; the Skill acts as a session-to-session cheat sheet.

---

## Connections

- [[concepts/model-context-protocol]] — "Connectors vs. Manuals" framing is the primary taxonomy in the concept page's MCP vs Skills section
