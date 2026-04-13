---
title: "Karpathy's LLM Wiki Pattern — Summary"
type: summary
source_count: 1
created: 2026-04-13
last_updated: 2026-04-13
tags: [pkm, knowledge-management, ai, llm, obsidian]
inbound_links: 0
status: complete
related_pages: ["[[concepts/llm-wiki-pattern]]", "[[entities/Obsidian]]", "[[topics/personal-knowledge-management]]"]
---

# Karpathy's LLM Wiki Pattern — Summary

**Author**: Andrej Karpathy
**Source**: gist (raw/articles/karpathy-llmwiki-pattern.md)
**Date**: Shared 2026

## One-Paragraph Summary

Instead of RAG (retrieving raw documents at query time), maintain a persistent LLM-written wiki that compiles and synthesizes knowledge incrementally. Three layers: raw sources (immutable), the wiki (LLM-generated Markdown), and a schema (CLAUDE.md governing conventions). Three operations: ingest (new source → 5-15 page updates), query (wiki-grounded answers that can be filed as new pages), and lint (periodic health check). Obsidian is the IDE; the LLM is the programmer; the wiki is the codebase.

## Key Claims

- The wiki is a persistent, compounding artifact — cross-references already exist, contradictions already flagged
- The human curates sources and asks good questions; the LLM does all bookkeeping
- Good answers to queries should be filed as new analysis pages — queries compound the knowledge base
- index.md (content catalog) lets LLM navigate without embedding-based RAG at moderate scale
- log.md (append-only timeline) helps LLM understand recent context

## Applications

Personal growth, research, book reading, business knowledge, competitive analysis, course notes, hobby deep-dives — any domain where knowledge accumulates over time.

## Filing Status

- [x] This vault implements this pattern
