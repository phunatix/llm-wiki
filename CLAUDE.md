# CLAUDE.md — LLM Wiki Schema & Operations

This document defines the structure, conventions, and workflows for maintaining the LLM Wiki. It evolves as you discover what works best.

---

## 1. Wiki Architecture

### Raw Sources (Immutable)
- **Location**: `raw/` directory
- **Subdirectories**: `articles/`, `papers/`, `books/`, `videos/`, `notes/`, `assets/` (images, data)
- **Rules**: 
  - Never modified by the LLM
  - Source of truth for all knowledge
  - Original URLs/citations preserved in frontmatter

### The Wiki (LLM-Generated)
- **Location**: `wiki/` directory
- **Categories**:
  - `entities/` — people, organizations, systems (e.g., OpenAI, GPT-4, Transformer Architecture)
  - `concepts/` — ideas, methods, theories (e.g., Scaling Laws, In-Context Learning, RLHF)
  - `topics/` — higher-level areas (e.g., "LLM Inference", "Training Stability")
  - `summaries/` — one-source summaries (link to entity/concept pages)
  - `analyses/` — multi-source syntheses (e.g., "Timeline of Model Releases")
  - `sources/` — explicit source tracking and metadata

### Special Files
- `wiki/index.md` — content-oriented catalog (updated on every ingest)
- `wiki/log.md` — append-only chronological record
- `CLAUDE.md` — this schema file (evolves with your needs)

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
- `inbound_links`: Updated by linter to track importance
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

## 10. Tools & Optional Enhancements

- **Obsidian Graph View**: Visualize wiki connectivity; identify hubs and orphans
- **Dataview**: Query pages by frontmatter (e.g., `source_count > 5`)
- **Marp**: Generate presentations from wiki content
- **Search**: Use Ctrl+Shift+F in Obsidian; for large wikis, consider [qmd](https://github.com/tobi/qmd)
- **Version Control**: This wiki is a git repo; you get commit history for free

---

## 11. Evolving the Schema

This schema is **not final**. As you build the wiki:
- You'll discover page types that don't fit the template
- You'll refine naming conventions
- You'll adjust log/index formats
- **Update this document** as you go

Signal when you want to evolve the schema by saying:
> "The schema isn't working for X reason. Let's adjust it."

---

## Checklist: First Steps

- [ ] Create raw source directory structure
- [ ] Add your first source to `raw/`
- [ ] Read this CLAUDE.md fully (let me know if questions)
- [ ] Ingest first source (I'll walk through the workflow)
- [ ] Build out 5-10 core pages (entities, concepts)
- [ ] Review the graph view in Obsidian
- [ ] Refine the schema based on what you learn

**You're now ready to build.**
