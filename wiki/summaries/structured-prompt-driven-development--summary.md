---
title: "Summary: Structured-Prompt-Driven Development (SPDD)"
type: summary
source_count: 1
created: 2026-06-22
last_updated: 2026-06-22
tags: [ai-agents, coding-agents, prompts, thoughtworks, software-engineering]
inbound_links: 0
status: complete
related_pages: ["[[concepts/structured-prompt-driven-development]]", "[[concepts/spec-driven-development]]", "[[topics/ai-software-development]]"]
---

# Summary: Structured-Prompt-Driven Development (SPDD)

**Source**: Wei Zhang & Jessie Jie Xia, Thoughtworks (martinfowler.com), 2026-04-28
**URL**: https://martinfowler.com/articles/structured-prompt-driven/

---

## One-Paragraph Summary

Zhang and Xia describe SPDD, a method developed by Thoughtworks' Global IT Services that treats structured prompts as first-class, version-controlled delivery artifacts. The core structure is the REASONS Canvas — a seven-part specification (Requirements, Entities, Approach, Structure, Operations, Norms, Safeguards) that guides prompts from intent through design to execution with governance constraints. The workflow enforces a closed loop: logic corrections must update the prompt before touching code; refactoring updates code first then syncs back to the prompt. Demonstrated via a billing engine enhancement, the method achieved ~99% intent alignment on first generation.

---

## Key Insights

- **Prompts as delivery artifacts**: Not ad-hoc chats but assets that are version-controlled, reviewed, reused, improved — placed under same discipline as code
- **REASONS Canvas**: Seven dimensions from abstract (R-E-A-S) through concrete (O) to governance (N-S); executable blueprint down to method signatures
- **Two types of post-generation changes**: Logic corrections (behavior change) → update prompt first, then code; Refactoring (no behavior change) → update code first, then sync prompt
- **Closed loop at two scales**: Within-iteration (prompt↔code stay aligned) and across-iterations (accumulated assets become starting context for next cycle)
- **Three core skills**: Abstraction First (design before generate), Alignment (lock intent before code), Iterative Review (controlled loop, not one-shot)
- **Categorized as spec-anchored**: Fits Böckeler's taxonomy — prompts are governed, versioned team assets that evolve alongside code
- **openspdd CLI**: Open-source tool implementing the workflow as repeatable commands (analysis → canvas → generate → test → sync)
- **Fitness sweet spot**: Scaled standardized delivery + high compliance environments (★★★★★); poor fit for exploratory spikes or poorly-defined domains (★★☆☆☆ / ★☆☆☆☆)

---

## Closing Quote

> "In the AI era, software development isn't a contest of model IQ. It's a contest of engineer cognitive bandwidth — how clearly we can think, frame problems, and make decisions."

---

## Relevance to Wiki

- Major expansion of [[concepts/spec-driven-development]] — SPDD is the most detailed spec-anchored implementation documented so far
- Addresses the spec-once failure mode identified in earlier SDD sources by making prompt↔code sync a workflow requirement
- Extends [[topics/ai-software-development]] with concrete organizational-level practice (vs. individual-level productivity)
- Thoughtworks origin connects to [[summaries/harness-engineering-for-coding-agents--summary]] and [[summaries/humans-and-agents-software-loops--summary]]

---

## Source Metadata

| Field | Value |
|---|---|
| Authors | Wei Zhang, Jessie Jie Xia (Thoughtworks) |
| Published | 2026-04-28 |
| Type | Technical article (martinfowler.com) |
| Clipped | 2026-05-04 |
