---
title: "Summary: How to Build an AI Second Brain with Claude Code and Obsidian — MindStudio"
type: summary
source_count: 1
created: 2026-04-17
last_updated: 2026-04-17
tags:
  - summary
  - pkm
  - obsidian
  - claude-code
  - tutorial
source_file: "raw/inbox/How to Build an AI Second Brain with Claude Code and Obsidian.md"
related_pages:
  - concepts/llm-wiki-pattern
  - concepts/ai-memory-architecture
  - concepts/para-method
  - entities/Obsidian
  - topics/personal-knowledge-management
status: complete
---

# Summary: How to Build an AI Second Brain with Claude Code and Obsidian

**Source**: MindStudio Team — "How to Build an AI Second Brain with Claude Code and Obsidian"
**URL**: https://www.mindstudio.ai/blog/build-ai-second-brain-claude-code-obsidian-2
**Published**: 2026-04-02 | **Clipped**: 2026-04-16
**Type**: Tutorial / promotional blog post (MindStudio product marketing)

---

## What This Source Contains

A practical how-to guide for setting up a Claude Code + Obsidian "second brain" system. Covers vault structure, CLAUDE.md setup, three core workflows (daily notes, meeting notes, weekly review), and automation via shell scripts. Concludes with a pitch for MindStudio's Agent Skills SDK as a commercial extension.

*Note: This is the type of tutorial that "Stop Calling It Memory" ([[summaries/stop-calling-it-memory-summary]]) critiques. Both sources are in the wiki for a complete picture of the debate.*

---

## Key Takeaways

### CLAUDE.md as Orientation Document
The guide frames CLAUDE.md as Claude's "persistent context file" — covering vault structure, naming conventions, recurring task definitions, and current project context. Updated regularly as the vault evolves. This matches how this wiki uses CLAUDE.md (the file you're reading right now): as the schema and operations guide, not as a data store.

### Three Core Workflows

**1. Daily Note Workflow**
- Templater creates a daily note each morning (priorities, meeting notes, decisions, open questions)
- End-of-day Claude Code prompt: "Review today's Daily Note, extract open tasks, link to projects, add TL;DR summary"
- Over time, project files accumulate rich contextual history automatically

**2. Meeting Note Workflow**
- Pre-meeting: "Pull relevant notes from /People/[person].md and linked projects"
- Post-meeting: "Format rough notes, extract action items, append to contact and project files"
- Builds structured, searchable relationship history without manual filing

**3. Weekly Review Workflow**
- Prompt: "Review all Daily Notes this week. Summarize decisions, flag open tasks across days, identify active projects, write /Reviews/[date]-weekly.md"
- After months: a detailed record of how time was actually spent — useful for reviews, billing, and self-understanding

### Vault Structure Recommendations
- Consistent YAML frontmatter on every note (date, tags, project, status)
- Atomic notes: one idea per note
- Clear folder structure (PARA-adjacent: /Projects, /People, /Daily Notes, /Resources, /Archive)
- Obsidian wikilinks for connections; Dataview plugin for programmatic queries

### Practical Mistake List
- Inconsistent note structure → Claude guesses, unreliable results
- Overly broad prompts → specify time range, tags, output format
- Not updating CLAUDE.md → stale context = bad outputs
- Trying to automate everything at once → start with daily notes only
- Treating Claude Code as stateless → it has persistent access via the vault; use it

### The MindStudio Pitch
MindStudio sells an Agent Skills npm SDK with 120+ typed capabilities (`agent.sendEmail()`, `agent.searchGoogle()`, `agent.runWorkflow()`). The guide positions this as the "next step" for teams or non-developers wanting a no-code interface. Source credibility note: this is a commercial tutorial with a product pitch at the end.

---

## Connections to Existing Wiki

- **[[concepts/llm-wiki-pattern]]**: This tutorial describes essentially the same architectural pattern — Claude Code reads/writes Markdown files in a structured vault. The LLM Wiki pattern is a more principled version of this.
- **[[concepts/para-method]]**: The recommended vault structure (/Projects, /People, /Resources, /Archive) is PARA-adjacent, validating that approach for Claude Code workflows.
- **[[entities/Obsidian]]**: Practical confirmation that Obsidian's plugin ecosystem (Dataview, Templater) is critical for making the AI integration work well.
- **[[summaries/stop-calling-it-memory-summary]]**: This guide is the exact type of content Edwards critiques. Reading both together gives a balanced view.

---

## Source Quality Notes

- Commercial marketing content from MindStudio (conflict of interest: they sell a competing SDK)
- Practical advice is sound and aligns with other PKM sources in the wiki
- The "second brain" framing is the inflated version Edwards calls out; the actual workflows described are reasonable and limited
- No performance data or scale considerations included
