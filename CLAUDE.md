# CLAUDE.md — LLM Wiki Schema & Operations

This file provides guidance to Claude Code (claude.ai/code) when working in this repository. It defines the structure, conventions, and workflows for maintaining the LLM Wiki, and it is the authoritative, actively-maintained operating contract — see § 14 for how it relates to the other meta-documents in this repo (`AGENTS.md`, `ARCHITECTURE.md`, `GEMINI.md`, etc.). It evolves as you discover what works best.

This is not a conventional application codebase — there is no code to build, lint, or test in the wiki itself. The "development workflow" is the ingest/query/lint loop described in § 6, and the only real tooling in the repo is the Quartz publishing pipeline (§ 13).

---

## 1. Wiki Architecture

### Raw Sources (Immutable)
- **Location**: `raw/` directory
- **Subdirectories**: `inbox/` (unprocessed drops), `articles/`, `sources/` (canonical after ingest), `guides/`, `notes/`, `assets/` (images, data)
- **Rules**: 
  - Never modified by the LLM
  - Source of truth for all knowledge
  - Original URLs/citations preserved in frontmatter
  - After ingest, sources move from `inbox/` to `sources/` (on user request)

### The Wiki (LLM-Generated)
- **Location**: `wiki/` directory
- **Categories**:
  - `entities/` — people, organizations, systems (e.g., Humanitec, Backstage, Apple)
  - `concepts/` — ideas, methods, theories (e.g., golden paths, spec-driven development, agentic infrastructure)
  - `topics/` — higher-level areas (e.g., platform engineering, AI software development)
  - `summaries/` — one-source summaries (link to entity/concept pages)
  - `analyses/` — multi-source syntheses (e.g., comparisons, timelines)
  - `sources/` — explicit source tracking and metadata
- **Current scope**: despite the schema's generic examples above, the wiki's actual content has converged on platform engineering and its adjacent systems — internal developer platforms, Kubernetes/homelab ops, SRE, AI-assisted/agentic software development, and the organizational choices around them — plus smaller side-topics (leadership, EVs, marathon training). `wiki/meta/overview.md` is the authoritative statement of current scope; check it before assuming domain from this file's illustrative examples.

### Special Files
- `wiki/index.md` — content-oriented catalog (updated on every ingest)
- `wiki/log.md` — append-only chronological record
- `wiki/meta/overview.md` — current scope, goals, and major themes
- `CLAUDE.md` — this schema file (evolves with your needs)

### Publishing Layer (Quartz)
- **Location**: `quartz/` directory (Quartz v4.5.2)
- **Purpose**: Publishes the `wiki/` directory as a static site to GitHub Pages
- **URL**: `phunatix.github.io/llm-wiki`
- **CI/CD**: `.github/workflows/deploy.yml` — auto-deploys on push to `main`
- **Build command**: `npx quartz build -d ../wiki` (run from `quartz/`)
- **Local preview**: `npm run serve` (from `quartz/`)
- **Config files**:
  - `quartz/quartz.config.ts` — site title, base URL, theme, plugins, ignore patterns
  - `quartz/quartz.layout.ts` — page layout components (sidebar, graph, TOC, backlinks)
- **Ignored by Quartz**: `private/`, `templates/`, `.obsidian/`, `log.md`
- **Key features**: SPA navigation, search, graph view, backlinks, dark mode, reader mode, RSS, sitemap, OG images, LaTeX (KaTeX)
- **Draft filtering**: Quartz `RemoveDrafts` plugin excludes pages with `draft: true` in frontmatter
- **Rules**:
  - Wiki content changes are the primary concern; Quartz config rarely needs changes
  - Quartz rebuilds the entire `wiki/` directory on each deploy — no manual build step needed
  - Do not commit `quartz/node_modules/`, `quartz/public/`, or `quartz/.quartz-cache/` (gitignored)

---

## 2. Page Frontmatter Convention

All wiki pages use YAML frontmatter:

```yaml
---
title: Page Title
type: entity|concept|topic|summary|analysis|source
source_count: 3
created: 2026-04-13
last_updated: 2026-04-13
tags: [tag1, tag2]
inbound_links: 5
status: complete|draft|needs-review
related_pages: ["[[entity/other-page]]", "[[concept/another-page]]"]
---
```

- `type`: Determines where the page lives and how it's formatted
- `source_count`: Number of raw sources cited on this page
- `created` / `last_updated`: For chronological tracking
- `tags`: Comma-separated for Dataview queries
- `inbound_links`: Intended to track importance, but there is no linter script in this repo that computes it automatically — despite `templates/README.md` describing it as linter-maintained, no such tool exists. In practice it's set once (usually to `0`) and rarely revisited; treat it as aspirational, not reliable, and don't cite it as a real popularity signal. Newer pages sometimes omit the field entirely (e.g. `wiki/entities/Backstage.md`), which is fine — it's not required by Quartz or by any check.
- `status`: complete = ready to cite; draft = under development; needs-review = marked for human review
- `related_pages`: Wikilinks to related pages (helps with cross-reference maintenance)

---

## 3. Page Types & Templates

### 3.1 Entity Pages
**Location**: `wiki/entities/[name].md`
**Purpose**: Information about a concrete thing (person, organization, model, system)
**Template**: See `templates/entity-template.md`

### 3.2 Concept Pages  
**Location**: `wiki/concepts/[name].md`
**Purpose**: An idea, method, or framework
**Template**: See `templates/concept-template.md`

### 3.3 Topic Pages
**Location**: `wiki/topics/[name].md`
**Purpose**: Higher-level organizing pages that aggregate related entities and concepts
**Template**: See `templates/topic-template.md`

### 3.4 Summary Pages
**Location**: `wiki/summaries/[source-title].md`
**Purpose**: One-paragraph summary of a raw source, with citations and key insights
**Template**: See `templates/summary-template.md`

### 3.5 Analysis Pages
**Location**: `wiki/analyses/[analysis-title].md`
**Purpose**: Multi-source synthesis, comparison, timeline, or deep analysis
**Template**: See `templates/analysis-template.md`

### 3.6 Source Pages
**Location**: `wiki/sources/[source-id].md`
**Purpose**: Metadata about a source (DOI, URL, access date, media type)
**Template**: See `templates/source-template.md`

---

## 4. Naming Conventions

- **Entity pages**: Proper names, title case (e.g., `OpenAI`, `GPT-4`, `Transformer Architecture`)
- **Concept pages**: Hyphenated, lowercase (e.g., `scaling-laws`, `in-context-learning`, `reinforcement-learning`)
- **Topic pages**: Hyphenated, lowercase (e.g., `llm-training`, `model-evaluation`)
- **Summary pages**: `[source-title]--summary` (e.g., `Attention-Is-All-You-Need--summary`)
- **Analysis pages**: Descriptive, hyphenated (e.g., `gpt-model-lineup-comparison`, `timeline-of-scaling-breakthroughs`)
- **Source pages**: `source-[unique-id]` (e.g., `source-arxiv-2410-12345`, `source-blog-karpathy-llm-history`)

---

## 5. Cross-Referencing

- Use **wikilinks** for all internal references: `[[entity/GPT-4]]`, `[[concept/scaling-laws]]`
- **Backlinks**: Obsidian auto-generates these; pages with many inbound links are hubs
- **Related pages**: List 3-5 most relevant pages in frontmatter `related_pages` field
- When ingesting: update ALL related pages with backlinks to the new page

---

## 6. Workflows

### 6.1 Ingest Workflow

**Input**: A new raw source (article, paper, video transcript, etc.)

**Steps**:
1. **Read the source** and identify key takeaways, entities, and concepts
2. **Discuss with user** — share a bullet-point summary; confirm what to emphasize
3. **Create/update entity pages** — for each mentioned person, org, system (create if missing, update if exists)
4. **Create/update concept pages** — for each idea or method introduced
5. **Create summary page** — short one-paragraph summary with key citations
6. **Update existing pages** — if new info updates or contradicts an existing page, revise and note the change
7. **Update `wiki/index.md`** — add new pages, increment source count for updated pages
8. **Append to `wiki/log.md`** — record the ingest event
9. **Review with user** — show diffs, confirm changes look right

**Expected result**: 5-15 wiki pages touched per source, index updated, log entry added.

### 6.2 Query Workflow

**Input**: A user question about the wiki content

**Steps**:
1. **Read `wiki/index.md`** — search for relevant pages
2. **Read target pages** — follow wikilinks to gather context
3. **Synthesize answer** — combine information across pages
4. **Consider filing** — if the answer is substantial (comparison, timeline, analysis), offer to file it as an analysis page
5. **Provide citations** — every claim traces back to a source in `raw/`

**Output**: Markdown answer with citations, optional new page to file into the wiki

### 6.3 Lint Workflow

**Input**: "Lint the wiki" (run periodically, e.g., monthly)

**Steps**:
1. **Check for contradictions** — look for conflicting claims across pages
2. **Find orphan pages** — pages with zero inbound links (may need deletion or linkage)
3. **Check staleness** — pages not updated in N months (may need review)
4. **Find missing pages** — concepts mentioned but lacking their own page
5. **Check reference integrity** — all wikilinks point to existing pages
6. **Suggest improvements** — what questions to ask, what sources to find, what connections to make
7. **Generate lint report** — summary of issues and suggestions

**Output**: Lint report; user prioritizes what to fix

---

## 7. Index Format (`wiki/index.md`)

The index is a **content-oriented catalog**. Format:

```markdown
# Wiki Index

**Updated**: 2026-04-13 | **Total Pages**: 42 | **Total Sources**: 8

## Entities (12)
- [[entities/OpenAI]] — Organization; founded 2015; created GPT series | Sources: 3
- [[entities/Ilya-Sutskever]] — Chief Scientist at OpenAI; researcher in ML safety | Sources: 2
- ...

## Concepts (18)
- [[concepts/scaling-laws]] — Empirical relationship between model size and loss | Sources: 5
- [[concepts/in-context-learning]] — Model's ability to learn from examples in-context | Sources: 4
- ...

## Topics (8)
- [[topics/llm-training]] — Covers pretraining, fine-tuning, RLHF | Pages: 12
- [[topics/model-evaluation]] — Benchmarks, evals, safety testing | Pages: 8
- ...

## Summaries (8)
- [[summaries/Attention-Is-All-You-Need--summary]] — Transformer architecture paper | Source: arxiv
- ...

## Analyses (2)
- [[analyses/gpt-model-lineup-comparison]] — GPT-2, 3, 3.5, 4 timeline and capabilities
- [[analyses/scaling-laws-synthesis]] — Multi-source synthesis of scaling trends
```

---

## 8. Log Format (`wiki/log.md`)

Append-only, with consistent prefix for parseability:

```markdown
# Wiki Evolution Log

## [2026-04-13] ingest | Attention Is All You Need (Vaswani et al.)
- Created `[[entities/Transformer-Architecture]]`
- Updated `[[concepts/attention-mechanism]]` with new citations
- Created `[[summaries/Attention-Is-All-You-Need--summary]]`
- **Key insight**: Introduces self-attention as core building block

## [2026-04-12] query | What are scaling laws?
- Referenced pages: `[[concepts/scaling-laws]]`, `[[analyses/scaling-laws-synthesis]]`
- Created `[[analyses/scaling-laws-synthesis]]` as new page filing

## [2026-04-10] lint | Monthly wiki health check
- Found 3 orphan pages; linked them
- Found 2 contradictions; resolved with user input
- Suggested 5 new source areas to explore
```

---

## 9. Guidelines for the LLM

### Do:
✓ Maintain **consistency** across pages (same fact stated the same way)
✓ **Update existing pages** when new info arrives (don't duplicate)
✓ **Create wikilinks** for every concept/entity mentioned
✓ **Preserve citations** — every claim has a source
✓ **Ask clarifying questions** if a source is ambiguous
✓ **Note contradictions** explicitly (e.g., "Source A claims X, Source B claims Y")
✓ **File good answers** into the wiki as analysis pages

### Don't:
✗ Create pages without citing a source
✗ Forget to update `index.md` and `log.md`
✗ Delete or modify pages in `raw/`
✗ Assume knowledge beyond what's in the wiki
✗ Leave broken wikilinks
✗ Mark pages complete if they're incomplete

---

## 10. Publishing with Quartz

The wiki is published as a static website via [Quartz v4](https://quartz.jzhao.xyz/).

### How it works
- Quartz reads all markdown files in `wiki/` and generates a static site
- Deployed automatically to GitHub Pages on every push to `main` via `.github/workflows/deploy.yml`
- Supports Obsidian-flavored markdown (wikilinks, callouts, etc.)

### Frontmatter considerations for publishing
- Pages with `draft: true` in frontmatter are excluded from the published site
- The `title` frontmatter field becomes the HTML page title
- Tags render as clickable links on the published site
- Dates use `frontmatter > git > filesystem` priority for "created" and "modified"

### What's excluded from publishing
- `templates/` — page templates (Quartz ignore pattern)
- `log.md` — internal operation log (Quartz ignore pattern)
- `.obsidian/` — Obsidian settings (Quartz ignore pattern)
- `private/` — any private content (Quartz ignore pattern)

### Local development
```bash
cd quartz
npm ci
npm run serve    # starts dev server at localhost:8080
```

### LLM guidelines for publishing
- When creating wiki pages, ensure frontmatter is valid YAML (Quartz will fail on malformed frontmatter)
- Use standard markdown image syntax or Obsidian embeds — Quartz handles both
- Wikilinks (`[[page]]`) work in Quartz; it resolves them using shortest-path matching
- Do not modify Quartz config or layout files unless explicitly asked

---

## 11. Tools & Integrations

### Authoring (Obsidian)
- **Graph View**: Visualize wiki connectivity; identify hubs and orphans
- **Dataview**: Query pages by frontmatter (e.g., `source_count > 5`)
- **Search**: Ctrl+Shift+F for full-text; Cmd+P for quick open

### Publishing (Quartz)
- **Site**: `phunatix.github.io/llm-wiki`
- **Search**: Full-text search built into the published site (FlexSearch)
- **Graph**: Interactive graph view on every page
- **Backlinks**: Auto-generated on the published site
- **RSS**: Available at `/index.xml`

### Infrastructure
- **Version Control**: Git — commit history for free
- **CI/CD**: GitHub Actions — deploy on push to `main`
- **Hosting**: GitHub Pages

---

## 12. Evolving the Schema

This schema is **not final**. As you build the wiki:
- You'll discover page types that don't fit the template
- You'll refine naming conventions
- You'll adjust log/index formats
- **Update this document** as you go

Signal when you want to evolve the schema by saying:
> "The schema isn't working for X reason. Let's adjust it."

---

## 13. Commands & Tooling

There is no build/lint/test step for the wiki content itself — it's plain markdown, and nothing checks it automatically except Quartz's build (which will fail loudly on malformed YAML frontmatter). The only real commands in this repo belong to the Quartz publishing layer, and you only need them when working on Quartz itself or verifying that a change will publish cleanly — not for routine ingest/query/lint work on `wiki/`.

All commands run from `quartz/` (Node ≥22, npm ≥10.9.2 — see `quartz/package.json` `engines`):

```bash
cd quartz
npm ci               # install dependencies (first time / after lockfile changes)
npm run build        # one-shot build: reads ../wiki, writes static site to quartz/public/
npm run serve        # build + serve locally with live reload (http://localhost:8080)
npm run check        # tsc --noEmit + prettier --check over Quartz's own source
npm run format       # prettier --write over Quartz's own source
npm test             # tsx --test — unit tests for Quartz internals, not wiki content
```

Notes:
- `npm run build` and `npm run serve` are the ones you'll actually use, e.g. to sanity-check that new frontmatter or a new page renders correctly before pushing.
- `npm run check` / `npm test` exercise the vendored Quartz framework code under `quartz/quartz/`, which this repo doesn't modify — only relevant if you're patching Quartz itself (rare; see § 10 rules).
- CI (`.github/workflows/deploy.yml`) runs `npm ci` + `npx quartz build -d ../wiki` on every push to `main` and deploys the result to GitHub Pages. There is no separate CI lint/test job — a broken build is the only thing that blocks a deploy.
- Wiki hygiene checks (broken wikilinks, orphan pages, stale `status`/frontmatter drift, index/page-count mismatches) are not backed by a checked-in script. They've historically been done with ad hoc `grep`/`find` one-liners during lint passes (§ 6.3) — see the pre-approved command patterns in `.claude/settings.json` for examples of the kind of query that's been used before.

---

## 14. Related Documents in This Repository

This repo has accumulated several overlapping meta-documents from different scaffolding sessions and tools. When they conflict, this file (`CLAUDE.md`) is authoritative for how to actually operate — the others range from complementary to stale:

- **`AGENTS.md`** — An earlier/parallel operating schema aimed at non-Claude coding agents (Codex, etc.). Its frontmatter schema (`status: active`, `source_files`, `updated`) and workflow details **differ** from what's actually in use (compare to real pages under `wiki/`, which follow this file's conventions: `status: complete|draft|needs-review`, `last_updated`, `related_pages`). Treat `AGENTS.md` as a looser, slightly out-of-sync sibling, not a second source of truth.
- **`GEMINI.md`** — A divergent schema apparently written for a different LLM/tool, describing conventions (e.g. a mandatory `### AI Insight` blockquote section on every ingest) that are **not** reflected anywhere in the actual wiki or in `wiki/log.md`'s history. It is not the contract this repo follows; don't adopt its conventions unless the user explicitly asks to.
- **`ARCHITECTURE.md`** — A descriptive system diagram/reference (layers, CI/CD pipeline, plugin pipeline, directory tree). Useful for orientation; update it if the directory structure or pipeline changes materially, but it's not itself a workflow contract.
- **`README.md`** — Short public-facing project overview.
- **`GETTING_STARTED.md`** / **`SETUP_COMPLETE.md`** — One-time onboarding docs written when the repo was first scaffolded (empty wiki, "ingest your first source"). They're historical artifacts of that first session, not current state — the wiki is well past that stage (see § 15). Don't use their checklists as a guide to what to do next.
- **`llmwiki.md`** — The original idea document (Andrej Karpathy's LLM-wiki pattern) that this repo was scaffolded from. Copied in verbatim as background reading; never edit it.
- **`templates/`** — Page-skeleton templates referenced throughout this file (§ 3, § 4). `templates/README.md` documents how to use them.

---

## 15. Current Snapshot

As of the last `wiki/log.md` entry (2026-07-11): **102 pages / 48 sources**, spanning 14 entities, ~31 concepts, 8 topics, 56 summaries, 23 source pages, and 1 analysis page. This will drift immediately as ingests continue — treat it as a rough sense of scale, not a live count. For the current numbers, read the header of `wiki/index.md` (`**Updated**: ... | **Total Pages**: ... | **Total Sources**: ...`) or run `find wiki -name '*.md' | grep -vE 'index.md|log.md' | wc -l`.
