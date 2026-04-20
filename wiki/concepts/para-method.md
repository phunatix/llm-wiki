---
title: PARA Method
type: concept
source_count: 1
created: 2026-04-16
last_updated: 2026-04-16
tags:
  - concept
  - pkm
  - note-taking
  - organization
related_pages:
  - concepts/johnny-decimal
  - concepts/llm-wiki-pattern
  - concepts/plain-text-first
  - topics/personal-knowledge-management
status: complete
---

# PARA Method

## Definition

PARA is a file and note organization framework created by **Tiago Forte**, introduced in his book *Building a Second Brain*. The acronym stands for:

- **P**rojects — Active work with a deadline and outcome
- **A**reas — Ongoing responsibilities without a defined end
- **R**esources — Reference material organized by topic
- **A**rchive — Inactive items from the other three categories

---

## Core Philosophy

PARA optimizes for **discoverability** — the ability to find and *reuse* knowledge when you need it, not just store it. Forte's argument: notes are only valuable if you encounter them again in a context where they're useful. A static, deeply nested hierarchy makes this nearly impossible. PARA's flexible structure allows items to migrate between buckets as their relevance changes:

- A "collaboration" that starts as a Resource may become a Project when it's active, then move to Archive when complete.
- An "Area" like fitness may spin up a Project ("run a marathon") and then recede.

The key contrast with sequential, static systems (like [[concepts/johnny-decimal|Johnny.Decimal]]): **PARA is organized around your current life, not around a taxonomy of topics.**

---

## Distinguishing Features

| Dimension | PARA | Johnny.Decimal |
|---|---|---|
| Optimizes for | Discoverability | Searchability |
| Structure | Flexible, movable | Static, hierarchical |
| Note-taking | Explicitly addressed | Not a primary use case |
| Number of top-level folders | 4 (always) | Many (10–20 areas) |
| Mental model | "What am I working on now?" | "Where does this belong?" |

---

## Strengths

- Explicitly integrates *note-taking* into the organizational system — not just file storage
- Keeps active projects front-and-center; reduces cognitive load of "where is that thing I was working on?"
- Interoperable: works in any tool (Obsidian, Notion, folder system)
- Scales from personal to professional use with the same four categories
- Encourages progressive summarization and synthesis — notes get refined over time, not just filed

---

## Limitations (from practitioner experience)

Crystal Lee (the source author) documented her shift from PARA → Johnny.Decimal → hybrid:
> "My brain just doesn't work that way, so I've slowly migrated back to Johnny.Decimal."

The flexibility that is PARA's strength is also its friction point: constantly deciding *where* something should move and *when* to archive it can itself become overhead. Not all brains find the four-folder model intuitive.

**Common tension**: PARA for *notes* (markdown, Obsidian) + a rigid system (like JD) for *files* (PDFs, downloads, documents) — a hybrid that several practitioners have landed on.

---

## Relation to the LLM Wiki Pattern

The [[concepts/llm-wiki-pattern|LLM Wiki Pattern]] is a layer above PARA. Where PARA organizes *your notes*, the LLM Wiki takes *raw sources* and compiles a structured, maintained knowledge graph. They are complementary:
- PARA: how you organize things you're actively working with
- LLM Wiki: how an AI maintains a persistent knowledge base from ingested sources

The wiki you're reading right now uses a PARA-adjacent taxonomy (entities / concepts / topics / summaries / analyses) that shares PARA's philosophy of prioritizing active use over perfect categorization.

---

## Related Pages

- [[concepts/johnny-decimal]] — The competing static-hierarchy approach
- [[concepts/llm-wiki-pattern]] — LLM-maintained wiki as a PARA evolution
- [[concepts/plain-text-first]] — Markdown as the ideal substrate for both PARA and LLM Wiki
- [[topics/personal-knowledge-management]] — Broader PKM context

---

*Source: Crystal Lee, "Two opinionated approaches to personal knowledge management" (2024-05-16)*
