# LLM Wiki Operating Schema

This repository is a persistent wiki maintained primarily by an LLM agent. Treat the markdown files in `wiki/` as the durable knowledge layer and the files in `raw/` as immutable source material.

## Core principles

- Prefer updating existing wiki pages over creating duplicate pages.
- Keep source files immutable. Never edit files under `raw/`.
- Use markdown links aggressively so pages form a navigable graph.
- Distinguish clearly between facts from sources, synthesis, and open questions.
- When new information conflicts with older material, preserve the conflict explicitly instead of silently overwriting it.
- Keep edits incremental and legible. A human should be able to inspect what changed and why.

## Repository contract

### Raw sources

- `raw/inbox/`: unprocessed source drops
- `raw/sources/`: canonical source files after ingestion
- `raw/assets/`: local images and attachments

### Wiki

- `wiki/index.md`: content-oriented catalog of important pages
- `wiki/log.md`: chronological operation log
- `wiki/meta/overview.md`: current scope, goals, and major themes
- `wiki/entities/`: entity pages
- `wiki/concepts/`: concept pages
- `wiki/sources/`: one page per ingested source
- `wiki/analyses/`: durable query outputs and syntheses

## Page conventions

Use YAML frontmatter on new wiki pages when practical:

```yaml
---
title: Page title
type: entity | concept | source | analysis | overview
status: active
created: YYYY-MM-DD
updated: YYYY-MM-DD
source_files:
  - raw/sources/example.md
tags:
  - tag
---
```

Then structure pages with some subset of:

- `# Summary`
- `# Key Facts`
- `# Relationships`
- `# Evidence`
- `# Open Questions`
- `# See Also`

Do not force this template mechanically. Adapt it to the page type.

## Linking rules

- Use wiki-relative markdown links, for example `[OpenAI](../entities/openai.md)`.
- Add a `See Also` section when a page materially relates to other pages.
- If a concept or entity is important enough to mention repeatedly, give it its own page.
- Avoid orphan pages: if a page exists, ensure something links to it and that it links outward where useful.

## Ingest workflow

When asked to ingest a new source:

1. Inspect `wiki/index.md` and relevant existing pages before writing.
2. Read the raw source file from `raw/inbox/` or `raw/sources/`.
3. Create or update a page under `wiki/sources/` summarizing the source.
4. Update any affected pages in `wiki/entities/`, `wiki/concepts/`, `wiki/analyses/`, or `wiki/meta/`.
5. Update `wiki/index.md` so the new or changed pages are discoverable.
6. Append a dated entry to `wiki/log.md` describing what changed.
7. If the source in `raw/inbox/` has been processed and the human requests cleanup, move it to `raw/sources/` rather than editing it.

## Query workflow

When asked a question about the wiki:

1. Start with `wiki/index.md`.
2. Read the most relevant linked pages.
3. Answer with explicit citations to the pages consulted.
4. If the answer produced a durable artifact, offer to file it under `wiki/analyses/`.
5. If you file it, also update `wiki/index.md` and `wiki/log.md`.

## Lint workflow

When asked to lint or health-check the wiki, look for:

- contradictions between pages
- stale claims superseded by newer sources
- missing pages for recurring entities or concepts
- weak or missing cross-links
- pages in `wiki/index.md` that no longer exist
- pages that exist but are absent from `wiki/index.md`
- open questions that suggest obvious next sources

Record meaningful lint outcomes in `wiki/log.md`.

## Editing rules

- Preserve human-written nuance; do not flatten uncertainty into false certainty.
- Prefer concise, information-dense prose over generic summary language.
- Do not fabricate citations or claim a source says something it does not say.
- If evidence is partial, label it as tentative.
- If the wiki's structure starts fighting the domain, update this file intentionally instead of improvising ad hoc exceptions forever.
