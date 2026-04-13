---
title: Eric J. Ma
type: entity
source_count: 1
created: 2026-04-13
last_updated: 2026-04-13
tags: [person, pkm, data-science, obsidian, ai]
inbound_links: 0
status: complete
related_pages: ["[[topics/personal-knowledge-management]]", "[[entities/Obsidian]]", "[[concepts/plain-text-first]]"]
---

# Eric J. Ma

**Category**: Person (Data Scientist / Blogger)

**Quick Summary**: Data scientist who documented a mature AI-augmented PKM system built on Obsidian; reduced knowledge management overhead from 30-40% to <10% of working time while managing 12 people.

## Overview

Eric J. Ma is a data scientist and blogger at MIT who manages 12 people across two teams. He documented a sophisticated personal knowledge management system built on Obsidian that uses AI coding agents (OpenCode) to maintain notes about people, projects, meetings, and technical context. His system is one of the most detailed public examples of the LLM-augmented PKM approach.

## Key System Components

- **People notes**: Dossiers for every direct report and frequent collaborator
- **Project notes**: Control towers linking to meetings, people, status
- **Meeting notes**: AI-formatted from transcripts via agent skill
- **Agent skills**: Encoded procedural knowledge in executable Markdown
- **AGENTS.md + HEARTBEAT.md**: Schema and sanity-check files, similar to CLAUDE.md

## Key Innovations

- **Progressive reveal for spreadsheets**: Agent maps structure before reading content — handles messy real-world Excel
- **Dual-path PowerPoint parsing**: XML structure + image captioning via VLM for ~90-95% accuracy
- **Retrieval practice**: Periodic sweeps to check what's missing or unsubstantiated in people/project notes
- **`uv` script metadata**: Each tool script declares its own dependencies inline (PEP 723) — no venv management

## Key Metrics

- PKM overhead: 30-40% of time → **<10% of time**
- Hallucination rate: ~1 in 4-5 sweeps; usually traces to bad transcript, not agent error
- People managed: 12, across 2 teams, each with 2-4 projects

## See Also

- [[topics/personal-knowledge-management]]
- [[entities/Obsidian]]
- [[concepts/plain-text-first]]
- [[concepts/llm-wiki-pattern]]

## Sources

- [[summaries/mastering-pkm-obsidian-ai--summary]]
