# LLM Wiki Architecture

A persistent, LLM-maintained knowledge base published as a static website.

---

## System Design

```
┌─────────────────────────────────────────────────────────────┐
│                        YOU (User)                           │
│  • Source sourcing & curation                               │
│  • Asking questions & setting priorities                    │
│  • Reviewing LLM-generated changes                         │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│                   CLAUDE (LLM Agent)                        │
│  • Reads sources and extracts knowledge                     │
│  • Updates wiki pages (create, revise, cross-reference)     │
│  • Maintains index and log                                  │
│  • Answers questions with wiki as context                   │
│  • Keeps wiki healthy (linting)                             │
└────────────────────┬────────────────────────────────────────┘
                     │
        ┌────────────┼────────────────┐
        ▼            ▼                ▼
┌──────────────┐ ┌────────────────┐ ┌──────────────────────┐
│ raw/         │ │ wiki/          │ │ quartz/              │
│ (Sources)    │ │ (Knowledge)    │ │ (Publishing)         │
│ ──────────── │ │ ────────────── │ │ ──────────────────── │
│ Immutable    │ │ LLM-generated  │ │ Quartz v4.5.2        │
│ Source of    │ │ Persistent     │ │ Static site builder   │
│ truth        │ │ artifact       │ │                      │
│              │ │                │ │ Reads wiki/ →        │
│ inbox/       │ │ entities/      │ │ builds HTML →        │
│ articles/    │ │ concepts/      │ │ deploys to           │
│ sources/     │ │ topics/        │ │ GitHub Pages         │
│ guides/      │ │ summaries/     │ │                      │
│ notes/       │ │ analyses/      │ │ Config:              │
│ assets/      │ │ sources/       │ │  quartz.config.ts    │
│              │ │ meta/          │ │  quartz.layout.ts    │
│              │ │ index.md       │ │                      │
│              │ │ log.md         │ │ CI/CD:               │
│              │ │                │ │  deploy.yml          │
└──────────────┘ └───────┬────────┘ └──────────┬───────────┘
                         │                     │
                  (Obsidian reads/      (auto-publishes
                   browses locally)      to the web)
                                               │
                                               ▼
                                  ┌────────────────────────┐
                                  │ phunatix.github.io/    │
                                  │ llm-wiki               │
                                  │ ────────────────────── │
                                  │ Static site with:      │
                                  │  • Full-text search    │
                                  │  • Interactive graph   │
                                  │  • Backlinks           │
                                  │  • Dark mode           │
                                  │  • RSS feed            │
                                  └────────────────────────┘
```

---

## Four Layers

### Layer 1: Raw Sources (`raw/`)
**Purpose**: Immutable source of truth

- **inbox/** — Unprocessed source drops (Web Clipper, manual adds)
- **articles/** — Blog posts, web articles (curated from inbox)
- **sources/** — Canonical source files after ingest
- **guides/** — How-to guides and tutorials
- **notes/** — Curated notes and miscellaneous
- **assets/** — Images, data files, diagrams

**Rules**:
- Never modified by the LLM
- Original citations and URLs preserved
- After ingest, sources move from `inbox/` to `sources/` (on user request)

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
- **log.md** — Append-only activity timeline
- **meta/overview.md** — Current scope, goals, and major themes

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

### Layer 3: Publishing (`quartz/`)
**Purpose**: Publishes the wiki as a static website

**Stack**: Quartz v4.5.2 (TypeScript, Preact, esbuild)

**How it works**:
1. Quartz reads all markdown files in `wiki/`
2. Transforms them using a plugin pipeline (frontmatter, syntax highlighting, wikilink resolution, LaTeX, etc.)
3. Generates static HTML, CSS, JS to `quartz/public/`
4. GitHub Actions deploys `public/` to GitHub Pages on every push to `main`

**Key configuration** (`quartz.config.ts`):
- Page title: "LLM Wiki"
- Base URL: `phunatix.github.io/llm-wiki`
- SPA mode enabled (client-side navigation)
- Popovers enabled (link preview on hover)
- Ignored: `private/`, `templates/`, `.obsidian/`, `log.md`
- Draft filtering: pages with `draft: true` are excluded

**Layout** (`quartz.layout.ts`):
- **Left sidebar**: Page title, search, dark mode toggle, reader mode, file explorer
- **Right sidebar**: Interactive graph, table of contents, backlinks
- **Content area**: Breadcrumbs, article title, metadata, tags, body

**Plugin pipeline**:
| Stage | Plugins |
|-------|---------|
| Transform | FrontMatter, CreatedModifiedDate, SyntaxHighlighting, ObsidianFlavoredMarkdown, GitHubFlavoredMarkdown, TableOfContents, CrawlLinks, Description, Latex |
| Filter | RemoveDrafts |
| Emit | AliasRedirects, ContentPage, FolderPage, TagPage, ContentIndex (sitemap + RSS), Assets, Static, Favicon, NotFoundPage, CustomOgImages |

**Build artifacts** (all gitignored):
- `quartz/node_modules/`
- `quartz/public/`
- `quartz/.quartz-cache/`

### Layer 4: Schema (`CLAUDE.md`, `AGENTS.md`)
**Purpose**: Governs how the LLM maintains the wiki

- **Directory structure** rules
- **Naming conventions** for pages
- **Page types** and their purposes
- **Cross-referencing** patterns
- **Workflows** (ingest, query, lint)
- **Index format** and update rules
- **Log format** and entry patterns
- **LLM guidelines** (do's and don'ts)
- **Publishing guidelines** (frontmatter, draft status)

---

## CI/CD Pipeline

```
Push to main
     │
     ▼
┌─────────────────────────────────────────┐
│ GitHub Actions: deploy.yml              │
│                                         │
│  build job (ubuntu-22.04):              │
│    1. Checkout repo (full history)      │
│    2. Setup Node.js 22                  │
│    3. npm ci (in quartz/)               │
│    4. npx quartz build -d ../wiki       │
│    5. Upload quartz/public/ as artifact │
│                                         │
│  deploy job:                            │
│    1. Deploy artifact to GitHub Pages   │
└─────────────────────────────────────────┘
     │
     ▼
  Live at phunatix.github.io/llm-wiki
```

---

## Core Workflows

### Ingest (Add a new source)
```
Raw source added to raw/inbox/
        │
        ▼
Claude reads the source
        │
        ▼
Claude & you discuss key takeaways
        │
        ▼
Claude creates/updates entity pages
Claude creates/updates concept pages
Claude creates summary page
Claude updates related pages
        │
        ▼
Claude updates wiki/index.md
Claude appends to wiki/log.md
        │
        ▼
You review diffs
        │
        ▼
Push to main → auto-deploys to site
```

### Query (Ask a question)
```
Your question
        │
        ▼
Claude reads wiki/index.md (catalog)
        │
        ▼
Claude identifies relevant pages
Claude reads those pages + wikilinks
        │
        ▼
Claude synthesizes answer with citations
        │
        ▼
Good answer? → Can file as new analysis page
```

### Lint (Maintain wiki health)
```
"Lint the wiki"
        │
        ▼
Claude checks for:
  • Contradictions across pages
  • Orphan pages (no inbound links)
  • Stale claims (not updated in months)
  • Missing pages (concepts mentioned but lacking page)
  • Broken wikilinks
  • Malformed frontmatter (would break Quartz build)
        │
        ▼
Claude generates lint report
You prioritize fixes
```

---

## Directory Structure

```
llm-wiki/
├── CLAUDE.md                    # LLM schema & operations
├── AGENTS.md                    # LLM operating contract
├── ARCHITECTURE.md              # This file
├── README.md                    # Project overview
├── .github/
│   └── workflows/
│       └── deploy.yml           # Quartz → GitHub Pages CI/CD
├── .gitignore                   # Ignores node_modules, public, .obsidian
├── raw/                         # Immutable source material
│   ├── inbox/                   #   Unprocessed drops
│   ├── articles/                #   Curated articles
│   ├── sources/                 #   Canonical post-ingest sources
│   ├── guides/                  #   How-to guides
│   ├── notes/                   #   Misc notes
│   └── assets/                  #   Images, data
├── wiki/                        # LLM-generated knowledge base
│   ├── index.md                 #   Content catalog
│   ├── log.md                   #   Activity timeline
│   ├── meta/                    #   Scope & overview
│   ├── entities/                #   People, orgs, systems
│   ├── concepts/                #   Ideas, methods, frameworks
│   ├── topics/                  #   High-level organizing areas
│   ├── summaries/               #   One-source summaries
│   ├── analyses/                #   Multi-source syntheses
│   └── sources/                 #   Source metadata pages
├── templates/                   # Page templates (not published)
├── quartz/                      # Quartz v4.5.2 static site builder
│   ├── quartz.config.ts         #   Site config (title, URL, plugins)
│   ├── quartz.layout.ts         #   Page layout (sidebar, graph, TOC)
│   ├── package.json             #   Node dependencies
│   ├── quartz/                  #   Quartz framework source
│   │   ├── components/          #     UI components (Preact)
│   │   ├── plugins/             #     Transform/filter/emit plugins
│   │   ├── styles/              #     SCSS stylesheets
│   │   └── util/                #     Shared utilities
│   ├── node_modules/            #   (gitignored)
│   └── public/                  #   (gitignored) build output
├── .obsidian/                   # Obsidian vault settings (gitignored)
├── .claude/                     # Claude Code settings
└── Clippings/                   # Obsidian Web Clipper output
```

---

## Cross-Referencing Strategy

**Wikilinks**: Every entity, concept, and related page uses `[[page-name]]` links

- Obsidian auto-generates backlinks for local browsing
- Quartz resolves wikilinks using shortest-path matching for the published site
- Both render interactive graph views showing page connectivity
- Pages with many inbound links are "hubs"
- Pages with zero inbound links are orphans (caught by linting)

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
| Raw | `raw/[category]/` | `karpathy-llmwiki-pattern.md` | Descriptive |

---

## Integrations

| Tool | Purpose | Context |
|------|---------|---------|
| **Obsidian** | Local authoring, browsing, graph view | Primary user interface |
| **Quartz** | Static site generation from markdown | Publishing layer |
| **GitHub Pages** | Hosting the published wiki | `phunatix.github.io/llm-wiki` |
| **GitHub Actions** | CI/CD — build and deploy on push | `.github/workflows/deploy.yml` |
| **Git** | Version control, commit history | Built into the workflow |
| **Web Clipper** | Capture articles into `raw/inbox/` | Browser extension → Obsidian |
| **Dataview** | Query pages by frontmatter metadata | Obsidian plugin |

---

## Philosophy

> "The tedious part of maintaining a knowledge base is not the reading or the thinking — it's the bookkeeping. Updating cross-references, keeping summaries current, noting when new data contradicts old claims, maintaining consistency across dozens of pages. Humans abandon wikis because the maintenance burden grows faster than the value. **LLMs don't get bored, don't forget to update a cross-reference, and can touch 15 files in one pass.** The wiki stays maintained because the cost of maintenance is near zero." — Andrej Karpathy

---

**Your role**: Curate sources and ask good questions.
**My role**: Do all the grunt work — read, extract, organize, maintain, cross-reference.
**Obsidian**: Your IDE for reading and exploring the wiki locally.
**Quartz**: Your pipeline for sharing the wiki with the world.
