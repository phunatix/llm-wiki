---
title: Personal Knowledge Management (PKM)
type: topic
source_count: 3
created: 2026-04-13
last_updated: 2026-04-13
tags: [pkm, obsidian, knowledge-management, note-taking, ai]
inbound_links: 0
status: complete
related_pages: ["[[entities/Obsidian]]", "[[concepts/plain-text-first]]", "[[concepts/llm-wiki-pattern]]"]
---

# Personal Knowledge Management (PKM)

**Scope**: Systems and practices for capturing, organizing, and retrieving personal knowledge — with a focus on Obsidian-based workflows and AI-augmented maintenance.

**Overview**: PKM is moving from passive note archiving to active, AI-maintained knowledge bases. The shift: rather than searching raw notes at query time, AI incrementally compiles and maintains a structured wiki that compounds over time. Obsidian's plain-text, local-first approach proves to be the ideal substrate for AI-augmented PKM.

## What's Included

- Obsidian as a PKM platform
- AI-augmented note maintenance (the LLM Wiki pattern)
- Read-it-later workflows in Obsidian
- Agent skills for knowledge management
- Information lifecycle: ingest → maintain → produce

## Core Concepts

- [[concepts/plain-text-first]]: Choosing plain text/Markdown for future-proofing and AI compatibility
- [[concepts/llm-wiki-pattern]]: Karpathy's pattern for LLM-maintained persistent wikis
- [[concepts/agent-skills]]: Encoded procedural knowledge that an AI coding agent executes

## Key Entities

- [[entities/Obsidian]]: The Markdown-based PKM tool at the center of these workflows
- [[entities/Eric-J-Ma]]: Data scientist; documented mature PKM system managing 12 people with reduced overhead
- Andrej Karpathy: ML researcher; originated the LLM Wiki pattern

## Landscape Map

```
PKM Spectrum
├── Read-it-later (Pocket, Instapaper → Obsidian + ReadItLater plugin)
├── Note-taking (manual notes, daily journals)
├── Structured PKM (Forte's PARA, Zettelkasten)
├── AI-augmented PKM (agent maintains notes from transcripts)
└── LLM Wiki (agent builds persistent, interlinked wiki from raw sources)

Human Effort Required: HIGH ──────────────────────────────── LOW
Knowledge Compounding: LOW  ──────────────────────────────── HIGH
```

## Key Insights

- Plain text (Markdown) is the right format for the 2025-2026 AI era — files agents can process natively, no migration needed
- The LLM Wiki pattern shifts from RAG (retrieve raw docs at query time) to a compiled, maintained knowledge graph
- Obsidian's graph view reveals the shape of your knowledge — hubs, orphans, clusters
- Agent skills encode procedural knowledge once, then execute repeatedly — overhead compounds down
- The key friction point: getting diverse formats (PDF, PPTX, video, spreadsheet) into plain text for agent processing
- PKM overhead can drop from 30-40% to <10% of working time with the right AI integration

## Key Debates

- **Privacy vs. cloud**: Local-first (Obsidian) vs. cloud-based tools (Notion, Confluence)
- **Structure vs. emergence**: How much template/schema to impose vs. letting connections emerge organically
- **Agent autonomy**: How much to verify agent-written notes vs. trusting and sweeping periodically

## See Also

- [[topics/ai-software-development]]: AI tools transforming knowledge work broadly
- [[concepts/llm-wiki-pattern]]: The specific pattern this wiki implements

## Sources by Relevance

- [[summaries/mastering-pkm-obsidian-ai--summary]]: Most detailed account of production PKM system with AI
- [[summaries/obsidian-read-it-later--summary]]: Lightweight workflow for using Obsidian as read-it-later app
- [[summaries/karpathy-llmwiki-pattern--summary]]: The foundational LLM Wiki pattern this vault implements
