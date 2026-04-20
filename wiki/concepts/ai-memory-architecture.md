---
title: AI Memory Architecture
type: concept
source_count: 2
created: 2026-04-17
last_updated: 2026-04-17
tags:
  - concept
  - pkm
  - ai-agents
  - databases
  - obsidian
related_pages:
  - concepts/llm-wiki-pattern
  - concepts/plain-text-first
  - concepts/para-method
  - topics/personal-knowledge-management
status: complete
---

# AI Memory Architecture

## The Core Question

How should a personal AI agent store and retrieve knowledge between sessions? Two dominant approaches have emerged, with sharp trade-offs:

| | Markdown-First | Database-First |
|---|---|---|
| **Storage** | `.md` files in a folder | SQLite, PostgreSQL, graph DB |
| **Setup cost** | Near-zero | Hours (schema design + tooling) |
| **Querying** | Read files into context window | SQL / Cypher traversal |
| **Relationships** | Wikilinks (visual only) | Graph DB (queryable traversal) |
| **Schema** | None (free-form text) | Enforced structure |
| **Scale ceiling** | ~500 notes before context bloat | Millions of records |
| **Concurrency** | Unsafe (file conflicts) | Native (WAL mode in SQLite) |
| **Human-readable** | Yes | Requires tooling |
| **Local-first** | Yes | Yes (SQLite, Kuzu) |
| **AI-readable** | Yes (natively) | Via SQL/query layer |

---

## The Markdown-First Case

Proponents: Karpathy (LLM Wiki pattern), Obsidian community, MindStudio AI second brain tutorial.

**Legitimate strengths**:
- LLMs read Markdown natively — no translation layer, no API, zero friction
- Human-readable and human-editable: you can inspect exactly what your AI "knows"
- Zero setup cost: `claude` in your vault directory, done
- Git-friendly: diffable, branchable, full history
- Local-first data sovereignty: files sit on your hard drive, no vendor lock-in
- Wikilinks create lightweight connections visible in graph view

**The [[concepts/llm-wiki-pattern|LLM Wiki pattern]]** uses this approach deliberately: the wiki is *human knowledge*, not machine records. Each page is written to be read by humans and AI alike. The goal is compounding knowledge across sources, not structured data management.

---

## The Database-First Case

Proponent: Jonathan Edwards ("Stop Calling It Memory," 2026).

**The critique**: Calling markdown files "AI memory" is a category error. The context window is not a query engine — it's a text buffer. Dumping files into context is brute force, not retrieval.

**Five failure modes of markdown-as-memory** (per Edwards):

1. **No querying** — Can't filter, sort, aggregate. "Show me all clients tagged 'video' in Philadelphia" requires reading every file and hoping Claude finds it.
2. **No relationships** — Wikilinks are visual, not traversable. Graph databases can run 2-hop relationship queries; markdown cannot.
3. **Scale ceiling** — At 500+ notes, you burn tokens on irrelevant context every session. At 5,000 notes, the system degrades the more you use it.
4. **No schema enforcement** — One session writes "## John Torres"; next session writes "**John T.** (Philly, video)". Inconsistent formatting breaks any attempt at structured retrieval.
5. **No concurrency** — Multiple agents writing the same file simultaneously silently corrupts data.

**Edwards' actual production system** (for comparison):
- SQLite: 955 structured memories across 22 categories, 832 KB — fully queryable
- Kuzu graph DB: 726 nodes, 852 relationships, 81 MB — traversable
- Total `.md` files: 636 lines across 4 files (all config/instructions, zero factual data)

**The sticky note analogy**: CLAUDE.md is a sticky note on the monitor — an instruction, a pointer. The actual data lives in spreadsheets and databases. Calling markdown files "AI memory" is like claiming the sticky note is the filing system.

---

## Reconciling the Two Views

The two camps are actually talking about *different use cases*:

**Markdown-first works well for**:
- A **knowledge wiki** — structured articles, summaries, analyses that humans also read and contribute to
- A **personal reading log** — capturing key ideas from sources over time
- A **note-taking system** — daily notes, meeting notes, project context
- Contexts where the AI helps you *write and organize*, not *query structured records*

**Database-first works well for**:
- A **CRM-style contact system** — structured records about people, projects, interactions
- **Autonomous agents** needing to store and retrieve operational state across sessions
- **Multi-agent systems** where concurrent writes are required
- Any use case requiring aggregation, filtering, or graph traversal at scale

**The architecture Edwards critiques** (markdown-as-agent-memory) is different from **the architecture this wiki uses** (markdown-as-knowledge-garden). The [[concepts/llm-wiki-pattern|LLM Wiki]] is not trying to be a database — it's a structured, human-readable, AI-maintained encyclopedia. It doesn't need to answer "show me all clients in Philadelphia"; it needs to answer "what do we know about scaling laws?"

The honest position: **both tools are right for different jobs**. A hammer isn't wrong because it can't drive screws.

---

## Practical Guidance

**Use markdown (Obsidian/wiki) when**:
- Content is primarily narrative and conceptual
- Humans will read and contribute to the content
- Cross-referencing via wikilinks is the primary access pattern
- You want AI to help you *write and synthesize*, not *query records*

**Use SQLite when**:
- Data is structured (contacts, events, tasks, logs)
- You need filtering, sorting, aggregation
- Multiple agents need concurrent access
- Records must follow a consistent schema

**Use a graph database (Kuzu, Neo4j) when**:
- Relationship traversal is the primary query need
- You need to answer questions like "who do I know who works on this project type?"
- Entity connections are as important as entity attributes

---

## Related Pages

- [[concepts/llm-wiki-pattern]] — the markdown-first approach this wiki implements
- [[concepts/plain-text-first]] — philosophical case for Markdown
- [[concepts/para-method]] — PARA as a file organization method (also markdown-native)
- [[topics/personal-knowledge-management]] — broader PKM context

---

*Sources: Jonathan Edwards, "Stop Calling It Memory" (2026-03-23); MindStudio, "How to Build an AI Second Brain" (2026-04-02)*
