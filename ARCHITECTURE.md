# LLM Wiki Architecture

A complete implementation of Andrej Karpathy's personal knowledge base pattern.

---

## System Design

```
┌─────────────────────────────────────────────────────────────┐
│                        YOU (User)                            │
│  • Source sourcing & curation                                │
│  • Asking questions & setting priorities                     │
│  • Reviewing LLM-generated changes                           │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ↓
┌─────────────────────────────────────────────────────────────┐
│                   CLAUDE (LLM Agent)                         │
│  • Reads sources and extracts knowledge                      │
│  • Updates wiki pages (create, revise, cross-reference)      │
│  • Maintains index and log                                   │
│  • Answers questions with wiki as context                   │
│  • Keeps wiki healthy (linting)                             │
└────────────────────┬────────────────────────────────────────┘
                     │
        ┌────────────┴────────────┐
        ↓                         ↓
┌──────────────────┐  ┌────────────────────────┐
│  raw/ (Sources)  │  │  wiki/ (Knowledge)     │
│  ─────────────   │  │  ──────────────────    │
│  Immutable       │  │  LLM-generated         │
│  Source of truth │  │  Persistent artifact   │
│                  │  │                        │
│  articles/       │  │  entities/             │
│  papers/         │  │  concepts/             │
│  books/          │  │  topics/               │
│  videos/         │  │  summaries/            │
│  assets/         │  │  analyses/             │
│  ...             │  │  sources/              │
│                  │  │  index.md (catalog)    │
│                  │  │  log.md (timeline)     │
└──────────────────┘  └────────────────────────┘
                            ↑
                            │
                   (user reads/browses
                    in Obsidian)
```

---

## Three Layers

### Layer 1: Raw Sources (`raw/`)
**Purpose**: Immutable source of truth

- **articles/** — Blog posts, web articles (via Web Clipper)
- **papers/** — Academic papers and preprints (PDF)
- **books/** — Book chapters and excerpts
- **videos/** — Video transcripts and notes
- **notes/** — Curated notes and miscellaneous
- **assets/** — Images, data files, diagrams
- **README.md** — Source organization guide

**Rules**:
- Never modified by the LLM
- Original citations and URLs preserved
- Metadata comments added (source, author, date, type)

### Layer 2: The Wiki (`wiki/`)
**Purpose**: Structured, interlinked knowledge base

**Page Types**:
1. **entities/** — Concrete things (people, organizations, systems)
2. **concepts/** — Abstract ideas, methods, frameworks
3. **topics/** — Higher-level organizing areas
4. **summaries/** — One-source summaries with key takeaways
5. **analyses/** — Multi-source syntheses, comparisons, timelines
6. **sources/** — Source metadata and tracking

**Special Files**:
- **index.md** — Content-oriented catalog of all pages
  - Organized by type (entities, concepts, topics, etc.)
  - One-line summary + source count for each page
  - Updated on every ingest
  - Used for quick navigation

- **log.md** — Append-only activity timeline
  - Records ingests, queries, linting sessions
  - Parseable format: `## [YYYY-MM-DD] operation | description`
  - Helps LLM understand recent context

**Page Frontmatter** (All pages):
```yaml
---
title: Page Name
type: entity|concept|topic|summary|analysis|source
source_count: N
created: 2026-04-13
last_updated: 2026-04-13
tags: [tag1, tag2]
inbound_links: N
status: draft|complete|needs-review
related_pages: ["[[entity/X]]", "[[concept/Y]]"]
---
```

### Layer 3: Schema (`CLAUDE.md`)
**Purpose**: Governs how the LLM maintains the wiki

- **Directory structure** rules
- **Naming conventions** for pages
- **Page types** and their purposes
- **Cross-referencing** patterns
- **Workflows** (ingest, query, lint)
- **Index format** and update rules
- **Log format** and entry patterns
- **LLM guidelines** (do's and don'ts)
- **Evolution plan** (how to improve the schema)

---

## Core Workflows

### Ingest (Add a new source)
```
Raw source added to raw/
        ↓
Claude reads the source
        ↓
Claude & you discuss key takeaways
        ↓
Claude creates/updates entity pages
Claude creates/updates concept pages
Claude creates summary page
Claude updates related pages
        ↓
Claude updates wiki/index.md
Claude appends to wiki/log.md
        ↓
You review diffs
        ↓
Wiki enriched by 5-15 page updates
```

**Result**: Single source touches multiple pages. Knowledge compounds.

### Query (Ask a question)
```
Your question
        ↓
Claude reads wiki/index.md (catalog)
        ↓
Claude identifies relevant pages
Claude reads those pages + wikilinks
        ↓
Claude synthesizes answer with citations
        ↓
Good answer? → Can file as new analysis page
        ↓
You get answer + optional new wiki page
```

**Result**: Answers are grounded in the wiki. Good answers get filed for future queries.

### Lint (Maintain wiki health)
```
Your request: "Lint the wiki"
        ↓
Claude checks for:
  • Contradictions across pages
  • Orphan pages (no inbound links)
  • Stale claims (not updated in months)
  • Missing pages (concepts mentioned but lacking page)
  • Broken wikilinks
  • Data gaps
        ↓
Claude generates lint report
        ↓
You prioritize fixes
        ↓
Claude implements fixes, updates index/log
```

**Result**: Wiki stays healthy as it grows.

---

## Cross-Referencing Strategy

**Wikilinks**: Every entity, concept, and related page uses `[[page-name]]` links

**Benefits**:
- Obsidian auto-generates backlinks
- Graph view shows connectivity
- Pages with many inbound links are "hubs"
- Pages with zero inbound links are orphans
- Navigation is intuitive

**Maintenance**:
- LLM adds wikilinks when creating pages
- LLM updates related pages when new pages arrive
- Linting catches broken links and orphans

---

## File Naming Conventions

| Type | Location | Example | Notes |
|------|----------|---------|-------|
| Entity | `wiki/entities/` | `OpenAI.md` | Proper names, title case |
| Concept | `wiki/concepts/` | `scaling-laws.md` | Hyphenated, lowercase |
| Topic | `wiki/topics/` | `llm-training.md` | Hyphenated, lowercase |
| Summary | `wiki/summaries/` | `Attention-Is-All-You-Need--summary.md` | Source-title--summary |
| Analysis | `wiki/analyses/` | `gpt-timeline-comparison.md` | Descriptive, hyphenated |
| Source | `wiki/sources/` | `source-arxiv-2410-12345.md` | source-unique-id |
| Raw | `raw/[category]/` | `karpathy-llmwiki-pattern.md` | Descriptive, preserve-extension |

---

## Data Flow on Ingest

```
raw/articles/new-source.md (immutable)
        ↓
Claude reads & discusses
        ↓
Creates/updates:
  • wiki/entities/Entity-1.md
  • wiki/entities/Entity-2.md
  • wiki/concepts/Concept-1.md
  • wiki/concepts/Concept-2.md
  • wiki/topics/Topic-1.md (updated)
  • wiki/summaries/new-source--summary.md
  • wiki/sources/source-unique-id.md
        ↓
Updates:
  • wiki/index.md (adds entries, increments source counts)
  • wiki/log.md (appends ingest record)
        ↓
Result: Source and its ideas are now integrated
        into the wiki's graph of knowledge
```

---

## Obsidian Integration

| Feature | Key Combo | Purpose |
|---------|-----------|---------|
| Graph View | Cmd+Shift+G | Visualize wiki structure; find hubs and orphans |
| Backlinks | Ctrl+Alt+L | See all pages linking to current page |
| Quick Open | Cmd+P | Jump to any page by name |
| Search | Ctrl+Shift+F | Find pages by content (full-text) |
| Wikilinks | `[[name]]` | Click-through navigation |
| Dataview | Code blocks | Query pages by frontmatter metadata |

---

## Growth Trajectory

| Phase | Sources | Pages | Key Activity |
|-------|---------|-------|--------------|
| **Seed** (Week 1) | 2-3 | 10-20 | Establish patterns; refine schema |
| **Growth** (Month 1) | 5-10 | 30-80 | Build core entities/concepts; see connections |
| **Maturity** (Month 3+) | 20+ | 100+ | Rich cross-references; regular linting; filing queries as pages |

---

## Optional Enhancements

- **Dataview Plugin**: Query pages by YAML metadata
- **Marp Plugin**: Generate presentations from wiki pages
- **qmd**: Local full-text search with vector re-ranking
- **Git**: Version control built-in (you get commit history free)
- **Obsidian Publish**: Share your wiki online

---

## Philosophy

> "The tedious part of maintaining a knowledge base is not the reading or the thinking — it's the bookkeeping. Updating cross-references, keeping summaries current, noting when new data contradicts old claims, maintaining consistency across dozens of pages. Humans abandon wikis because the maintenance burden grows faster than the value. **LLMs don't get bored, don't forget to update a cross-reference, and can touch 15 files in one pass.** The wiki stays maintained because the cost of maintenance is near zero." — Andrej Karpathy

---

**Your role**: Curate sources and ask good questions.
**My role**: Do all the grunt work — read, extract, organize, maintain, cross-reference.
**Obsidian**: Your IDE for reading and exploring the wiki.

This is a collaboration where each party does what it does best.
