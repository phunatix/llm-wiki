# LLM Wiki

A markdown-first repository for maintaining a personal knowledge base with an LLM as the primary editor.

The repo is organized into three layers:

- `raw/`: immutable source material
- `wiki/`: LLM-maintained markdown knowledge base
- `AGENTS.md`: operating schema for the LLM

## Layout

- `raw/inbox/`: newly added sources awaiting processing
- `raw/sources/`: canonical raw source files after triage
- `raw/assets/`: downloaded images and attachments referenced by sources
- `wiki/index.md`: catalog of wiki pages
- `wiki/log.md`: append-only operational log
- `wiki/meta/overview.md`: high-level description of the wiki's scope
- `wiki/entities/`: people, organizations, places, tools, books, products
- `wiki/concepts/`: ideas, themes, frameworks, domains
- `wiki/sources/`: one page per ingested source
- `wiki/analyses/`: filed answers, comparisons, reports, syntheses
- `templates/`: optional page templates for consistent page creation

## Typical workflow

1. Drop a new file into `raw/inbox/`.
2. Ask the LLM to ingest it.
3. The LLM reads `AGENTS.md`, updates the relevant pages in `wiki/`, and appends to `wiki/log.md`.
4. Query the wiki and file useful answers back into `wiki/analyses/`.

## Notes

- `llmwiki.md` is the source idea document used to scaffold this repo.
- The wiki is intended to be browsed in Obsidian or any markdown editor.
