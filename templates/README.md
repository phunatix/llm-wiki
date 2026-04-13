# Wiki Templates

This folder contains Markdown templates for each page type in the wiki. Use these as starting points when creating new pages.

## Template Files

- **entity-template.md** — Organizations, people, systems, models. Use for concrete things.
- **concept-template.md** — Ideas, methods, theories, frameworks. Use for abstract concepts.
- **topic-template.md** — Higher-level areas that aggregate related concepts and entities.
- **summary-template.md** — One-source summaries. Used when ingesting new raw sources.
- **analysis-template.md** — Multi-source synthesis, comparisons, timelines, deep dives.
- **source-template.md** — Metadata about raw sources (bibliographic info, links, reliability).

## How to Use

When creating a new page:
1. Copy the relevant template
2. Rename the file to match naming conventions (see CLAUDE.md § 4)
3. Place in the correct subdirectory under `wiki/`
4. Fill in the frontmatter
5. Complete all sections
6. Add wikilinks to related pages
7. Update `wiki/index.md` with the new page

## Template Philosophy

Templates are **guides, not rigid rules**. They capture common patterns but:
- You can add sections if your content needs them
- You can remove sections if they don't apply
- You can rename sections for clarity
- Update the templates themselves if you find better patterns

The goal is **consistency without dogmatism**.

## Frontmatter Fields

All templates use this standard frontmatter:

```yaml
---
title: Page Title
type: entity|concept|topic|summary|analysis|source
source_count: 0
created: 2026-04-13
last_updated: 2026-04-13
tags: []
inbound_links: 0
status: draft|complete|needs-review
related_pages: []
---
```

- **source_count**: How many raw sources cite this page
- **created/last_updated**: For chronological tracking
- **inbound_links**: Updated by linter; tracks how many other pages link to this one
- **status**: draft (in progress), complete (ready), needs-review (marked for human input)
- **related_pages**: Wikilinks to related pages

## See Also

- CLAUDE.md for full schema documentation
- wiki/index.md to see pages currently in the wiki
- wiki/log.md to see recent activity
