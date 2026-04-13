---
title: "Mastering PKM with Obsidian and AI — Summary"
type: summary
source_count: 1
created: 2026-04-13
last_updated: 2026-04-13
tags: [pkm, obsidian, ai, knowledge-management]
inbound_links: 0
status: complete
related_pages: ["[[entities/Obsidian]]", "[[entities/Eric-J-Ma]]", "[[concepts/plain-text-first]]", "[[concepts/llm-wiki-pattern]]", "[[topics/personal-knowledge-management]]"]
---

# Mastering PKM with Obsidian and AI — Summary

**Author**: Eric J. Ma
**Source**: ericmjl.github.io blog
**Date**: March 2026

## One-Paragraph Summary

A data scientist managing 12 people across 2 teams reduced PKM overhead from 30-40% to <10% of his time by building an Obsidian vault with AI coding agents (OpenCode) maintaining people notes, project notes, and meeting notes from raw sources. The system uses an AGENTS.md schema, agent "skills" (executable Markdown encoding procedural knowledge), and structured note types. Key innovations: progressive reveal for messy spreadsheets, dual-path PowerPoint parsing (XML + image captioning), and `uv` script metadata for dependency-free tool scripts.

## Key Claims

- Plain text (Markdown) proved ideal for AI augmentation — files agents process natively, no migration needed
- "Sweeps": agent updates people/project notes from source material; hallucinations rare (~1 in 4-5 sweeps)
- Agent skills compound over time — procedures encoded once, executed repeatedly, overhead trends down
- PKM overhead: 30-40% → <10% of working time
- openpyxl better than pandas for messy real-world spreadsheets (reads granular cell structure)
- Progressive reveal for large files: map structure first, then zoom in on relevant sections
- AGENTS.md + HEARTBEAT.md = schema + sanity check (similar to CLAUDE.md in this vault)

## Key Tools

- **OpenCode**: AI coding agent used for vault maintenance
- **python-docx**: Word → plain text
- **python-pptx + LibreOffice + PIL + VLM**: PowerPoint → images → captions → narrative (~90-95% accurate)
- **openpyxl**: Excel → structured reading
- **uv + PEP 723**: Dependency-isolated tool scripts, no venv management

## Filing Status

- [x] All sections complete
