---
title: LLM Wiki Pattern
type: concept
source_count: 2
created: 2026-04-13
last_updated: 2026-04-13
tags: [pkm, knowledge-management, ai, llm, obsidian]
inbound_links: 0
status: complete
related_pages: ["[[entities/Obsidian]]", "[[concepts/plain-text-first]]", "[[topics/personal-knowledge-management]]"]
---

# LLM Wiki Pattern

**Domain**: Personal Knowledge Management / AI-Augmented Knowledge

**One-line definition**: A pattern where an LLM incrementally builds and maintains a persistent, interlinked wiki from raw sources — shifting from RAG (retrieval at query time) to compiled, maintained knowledge.

## The Core Insight

Most RAG systems rediscover knowledge from scratch on every query. The LLM Wiki pattern is different:

> **The wiki is a persistent, compounding artifact.** The cross-references are already there. The contradictions have already been flagged. The synthesis already reflects everything you've read. — Andrej Karpathy

Instead of retrieving from raw documents, the LLM reads each new source, extracts knowledge, and integrates it into the wiki — updating entity pages, concept pages, flagging contradictions, and maintaining cross-references.

## Three-Layer Architecture

1. **Raw Sources** (`raw/`): Immutable source of truth; articles, papers, books, etc.
2. **The Wiki** (`wiki/`): LLM-generated, interlinked Markdown pages; the compiled knowledge
3. **The Schema** (`CLAUDE.md`): Rules that govern how the LLM maintains the wiki

## Three Core Operations

- **Ingest**: New source → LLM reads → discusses → creates/updates 5-15 wiki pages → updates index/log
- **Query**: Question → LLM reads index → reads relevant pages → synthesizes answer → optionally files as new page
- **Lint**: Periodic health check → finds contradictions, orphans, staleness, missing links

## Key Navigation Files

- **`wiki/index.md`**: Content-oriented catalog; LLM reads this first when answering questions
- **`wiki/log.md`**: Append-only chronological record; helps LLM understand recent context

## Relationship to Andrej Karpathy

The pattern was described by Andrej Karpathy in a gist that became the seed source for this wiki. Key quote:

> "Obsidian is the IDE; the LLM is the programmer; the wiki is the codebase."

## Comparison with Eric J. Ma's System

[[entities/Eric-J-Ma]]'s system shares the same philosophy but focuses on professional/people context rather than topic research:
- People notes + project notes instead of entity/concept/topic pages
- Agent "sweeps" for maintenance vs. explicit ingest workflow
- Similar use of AGENTS.md schema file

## Why This Works

The maintenance cost of a knowledge base is the bottleneck — humans abandon wikis because upkeep grows faster than value. LLMs eliminate this bottleneck: they don't get bored, don't forget to update a cross-reference, can touch 15 files in one pass.

## See Also

- [[entities/Obsidian]]
- [[concepts/plain-text-first]]
- [[topics/personal-knowledge-management]]

## Sources

- [[summaries/karpathy-llmwiki-pattern--summary]]: Original pattern description
- [[summaries/mastering-pkm-obsidian-ai--summary]]: A related implementation in production
