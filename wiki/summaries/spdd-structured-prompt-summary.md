---
title: "Summary: Structured Prompt-Driven Development (SPDD)"
type: summary
source_count: 1
created: 2026-06-15
last_updated: 2026-06-15
tags: [summary, spec-driven-development, thoughtworks, methodology]
source_file: "raw/inbox/Structured-Prompt-Driven Development (SPDD).md"
related_pages:
  - concepts/spec-driven-development
  - topics/ai-software-development
status: complete
---

# Summary: Structured Prompt-Driven Development (SPDD)

**Source**: martinfowler.com — "Structured Prompt-Driven Development (SPDD)"
**Author**: Wei Zhang & Jessie Jie Xia (Thoughtworks Global IT Services)
**URL**: https://martinfowler.com/articles/structured-prompt-driven/
**Published**: 2026-04-28 | **Clipped**: 2026-05-04
**Type**: Methodology article with worked example

---

## Key Takeaways

**The problem SPDD addresses**: Individual AI coding speed doesn't translate to team-level throughput. Ambiguous requirements become code quickly and misunderstandings scale. Reviews process more change. Integration issues surface because "generated" doesn't mean "aligned." Like driving a Ferrari on muddy roads — engine is powerful, but arrival time is determined by road conditions.

**SPDD distinguishes itself from SDD** by treating prompts as first-class team artifacts: version-controlled, reviewed, reused, improved over time. It's spec-anchored by design.

**The REASONS Canvas** — seven-part structure for a prompt:
- R: Requirements (what + DoD)
- E: Entities (domain model)
- A: Approach (strategy)
- S: Structure (system placement + dependencies)
- O: Operations (concrete, testable steps)
- N: Norms (cross-cutting standards: naming, observability, defensive coding)
- S: Safeguards (invariants, security rules, performance limits)

**Core rule**: "When reality diverges, fix the prompt first — then update the code." This prevents prompt-code divergence.

**The closed loop**: Unlike one-way pipelines where specs become stale, SPDD closes the loop in both directions: code changes sync back to the prompt via `/spdd-sync`; prompt updates drive code changes via `/spdd-generate`. Accumulated prompt assets become the starting context for the next enhancement.

---

## Connections

- [[concepts/spec-driven-development]] — REASONS Canvas is the SPDD-specific implementation; Böckeler classifies SPDD as spec-anchored
