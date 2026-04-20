---
title: "Summary: Stop Calling It Memory — Jonathan Edwards"
type: summary
source_count: 1
created: 2026-04-17
last_updated: 2026-04-17
tags:
  - summary
  - pkm
  - ai-agents
  - databases
  - obsidian
  - critique
source_file: "raw/inbox/Stop Calling It Memory The Problem with Every \"AI + Obsidian\" Tutorial.md"
related_pages:
  - concepts/ai-memory-architecture
  - concepts/llm-wiki-pattern
  - concepts/plain-text-first
  - topics/personal-knowledge-management
status: complete
---

# Summary: Stop Calling It Memory

**Source**: Jonathan Edwards — "Stop Calling It Memory: The Problem with Every 'AI + Obsidian' Tutorial"
**URL**: https://limitededitionjonathan.substack.com/p/stop-calling-it-memory-the-problem
**Published**: 2026-03-23 | **Clipped**: 2026-04-16
**Type**: Critical Substack essay; practitioner perspective

---

## What This Source Contains

A sharp, technically grounded critique of the "Obsidian + Claude Code = AI memory" content trend that exploded in February–March 2026. The author documents the archaeology of how the trend spread, explains why markdown files cannot replace databases for AI agent memory, and presents his own production database-first architecture as an alternative.

---

## Key Takeaways

### The Influencer-to-Cargo-Cult Pipeline
The author traces a specific propagation chain:
1. Tiago Forte made "second brain" the default metaphor
2. Anthropic introduced CLAUDE.md (a config file) and Skills (prompt templates)
3. OpenClaw used MEMORY.md as memory storage — and had to bolt on SQLite + vector search underneath because markdown didn't work
4. Steph Ango (Obsidian CEO) released Agent Skills in January 2026 → 13.9K+ GitHub stars
5. Content creators in February–March 2026 ran with "markdown files = AI brain" without checking the foundations

The result: an entire content ecosystem where each post cited previous posts as validation, none questioning the foundational assumption.

### What Markdown Memory Systems Actually Do
The "memory" mechanism is:
1. Claude reads a `.md` file into its context window
2. Claude reads the information
3. Claude writes updates back to the file

This works at small scale. It fails at medium scale. It collapses at large scale. "The context window isn't a database. Treating it like one is like trying to run a restaurant kitchen by putting every ingredient on the counter at the same time."

### The Five Failure Modes (Will hit, not might hit)
1. **No querying** — Can't filter, sort, or aggregate. Only operation: "read file, hope Claude finds it."
2. **No relationships** — Wikilinks are visual. You can't traverse them programmatically or run multi-hop queries.
3. **Scale ceiling** — More context = more tokens burned, slower, more expensive, less accurate. Degrades with use.
4. **No schema enforcement** — Claude writes "## John Torres" one session, "**John T.** (Philly)" the next. Impossible to parse reliably.
5. **No concurrency** — Multiple agents writing the same `.md` file simultaneously silently corrupts data.

### His Production Architecture (Contrast)
- **SQLite** (832 KB): 955 structured memories, 22 categories, 67 email interactions, 49 session logs — all indexed, queryable
- **Kuzu graph DB** (81 MB): 726 nodes (475 people, 116 projects, 54 concepts, 43 tools), 852 relationships across 12 types
- **Total `.md` files**: 636 lines — CLAUDE.md is boot instructions, Skills are prompt templates. *Zero facts about his life stored in markdown.*

### The Sticky Note Analogy
> "CLAUDE.md is a sticky note on the monitor. The data is in the filing cabinet, the spreadsheets, the ERP system. Anthropic put a sticky note on Claude's monitor, and an entire content ecosystem decided that sticky notes were infrastructure."

### Alternatives That Actually Work
- **SQLite**: Zero setup server; single file; local-first; Claude Code writes SQL natively
- **Kuzu**: Local embedded graph DB; relationship traversal; no server
- **Open Brain (OB1)**: Nate Jones's Supabase-backed PKM; structured storage + vector search out of the box
- **Supabase**: PostgreSQL + vector search + real-time; self-hostable

### What Obsidian Is Actually Good For (Per Edwards)
Notes, knowledge garden, human-readable knowledge management — legitimate use. Obsidian is **not** a memory store for autonomous agents. The CLAUDE.md Agent Skills from Steph Ango are "well-designed and appropriately scoped" — format specifications for Obsidian's file formats, not a memory architecture.

---

## Relation to This Wiki

This source directly challenges the foundation this wiki uses. A fair reading:

**Edwards is right about**: Agent memory for structured operational data (contacts, tasks, logs). If you're building an autonomous agent that needs to remember 955 client interactions, markdown fails.

**The LLM Wiki is different**: This wiki isn't storing structured operational data. It's maintaining a *knowledge encyclopedia* — narrative articles that humans also read and edit. The access pattern is "read relevant pages and synthesize," not "query records and join tables." The [[concepts/llm-wiki-pattern|LLM Wiki pattern]] explicitly builds on the strengths Edwards acknowledges (native LLM readability, human transparency, zero friction) for the use case he exempts (note-taking, knowledge garden).

See [[concepts/ai-memory-architecture]] for a full reconciliation of both perspectives.

---

## New Concept Created

- [[concepts/ai-memory-architecture]] — the debate; when to use markdown vs. databases for AI agent knowledge
