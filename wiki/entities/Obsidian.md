---
title: Obsidian
type: entity
source_count: 3
created: 2026-04-13
last_updated: 2026-04-13
tags: [pkm, note-taking, tool, markdown, knowledge-management]
inbound_links: 0
status: complete
related_pages: ["[[concepts/plain-text-first]]", "[[concepts/llm-wiki-pattern]]", "[[topics/personal-knowledge-management]]"]
---

# Obsidian

**Category**: Software Tool (PKM / Note-taking)

**Quick Summary**: A local-first, Markdown-based personal knowledge management tool; its plain-text format proves ideal for AI-augmented PKM workflows.

## Overview

Obsidian stores all notes as plain Markdown files on your local disk. This design choice — simple, local, no vendor lock-in — turned out to be prescient for the AI era: coding agents can process these files natively without any conversion layer.

## Key Features for PKM

- **Graph view**: Visualizes links between notes — shows hubs, clusters, orphans
- **Wikilinks**: `[[note-name]]` creates navigable, bidirectional links
- **Backlinks**: Auto-generated list of every note linking to the current one
- **Dataview plugin**: Queries notes by YAML frontmatter (like a database over your vault)
- **Templates**: Reusable note structures
- **Community plugins**: ReadItLater, Share Note, Marp, etc.

## Relevant Plugins

- **ReadItLater**: Saves web articles from clipboard to vault as Markdown
- **Dataview**: SQL-like queries over frontmatter metadata
- **Marp**: Generates slide decks from Markdown
- **Web Clipper** (browser extension): Converts web articles to Markdown with one click

## Key Settings

- "Attachment folder path" → Set to `raw/assets/` to centralize media
- "Download attachments" hotkey → Downloads linked images to local storage

## Why Plain Text Matters (2025-2026 Context)

> "Text files are as primitive as it gets: no proprietary formats, no vendor lock-in, just files that can be read on any system. When AI coding agents arrived, my vault was already in a format they could process natively." — Eric J. Ma

## Use Patterns

1. **Read-it-later**: URL → ReadItLater plugin → Markdown in vault → tag as unread → Dataview list of unread
2. **Meeting notes**: Transcript → AI agent formats → structured note linked to people/project pages
3. **LLM Wiki**: Raw sources → AI agent reads → creates/updates wiki pages → graph view grows

## Relationships

- **Compatible with**: Claude Code, OpenCode, any AI agent that can read files
- **Alternative to**: Notion (cloud-first), Confluence (enterprise), Roam (proprietary)

## See Also

- [[concepts/plain-text-first]]
- [[concepts/llm-wiki-pattern]]
- [[topics/personal-knowledge-management]]

## Sources

- [[summaries/mastering-pkm-obsidian-ai--summary]]: Mature production PKM system built on Obsidian
- [[summaries/obsidian-read-it-later--summary]]: Obsidian as read-it-later replacement
- [[summaries/karpathy-llmwiki-pattern--summary]]: The LLM Wiki pattern that uses Obsidian as its IDE
