---
title: Plain Text First
type: concept
source_count: 2
created: 2026-04-13
last_updated: 2026-04-13
tags: [pkm, knowledge-management, ai, obsidian]
inbound_links: 0
status: complete
related_pages: ["[[entities/Obsidian]]", "[[concepts/llm-wiki-pattern]]", "[[topics/personal-knowledge-management]]"]
---

# Plain Text First

**Domain**: Personal Knowledge Management / Information Architecture

**One-line definition**: Choosing plain text (Markdown) as the primary storage format for personal knowledge — a decision that proved prescient as AI coding agents arrived and could process these files natively.

## Definition

Plain text first is the design philosophy of storing knowledge in the simplest, most portable format: plain Markdown files. No proprietary formats, no vendor lock-in, no database. Files that can be read on any system, by any tool, forever.

## Why It Proved Correct (2025-2026 Context)

> "Text files are as primitive as it gets... When AI coding agents arrived, my vault was already in a format they could process natively. No migration needed. No conversion layer. No API integration." — Eric J. Ma

The design choice made in 2022 (for its simplicity and graph view) became a major unlock in 2025-2026:
- AI agents can read and write Markdown directly
- No conversion, export, or API needed
- The "IDE" for your knowledge base is ready to use

## Implications for PKM Design

- **Local first**: Files on disk, not in a cloud database
- **Version control**: Git works natively — you get full history for free
- **Tool agnostic**: Any editor (Obsidian, VS Code, vim) can read your knowledge base
- **AI compatible**: Every AI coding agent speaks Markdown

## Converting Other Formats to Plain Text

When sources arrive in non-Markdown formats, convert them:
- **Word (.docx)**: python-docx → plain text
- **PowerPoint (.pptx)**: python-pptx (XML) + LibreOffice → images → VLM captions
- **PDF**: text extraction (text PDFs) or image captioning (scanned)
- **Excel**: openpyxl (not pandas) — reads granular cellular structure, handles messy real-world spreadsheets
- **Web articles**: Obsidian Web Clipper or ReadItLater plugin

## Obsidian as the Plain Text PKM

[[entities/Obsidian]] is the primary tool implementing this philosophy:
- All notes as `.md` files in a local directory (the "vault")
- Graph view, backlinks, and wikilinks work without any database
- AI agents can read and write the vault directly

## See Also

- [[entities/Obsidian]]
- [[concepts/llm-wiki-pattern]]
- [[topics/personal-knowledge-management]]

## Sources

- [[summaries/mastering-pkm-obsidian-ai--summary]]: Detailed case study of plain-text PKM in production
- [[summaries/obsidian-read-it-later--summary]]: Plain text as read-it-later format
