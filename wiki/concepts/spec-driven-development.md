---
title: Spec-Driven Development
type: concept
source_count: 4
created: 2026-06-15
last_updated: 2026-06-15
tags:
  - concept
  - ai-software-development
  - methodology
  - coding-agents
related_pages:
  - concepts/agentic-development-loop
  - concepts/harness-engineering
  - concepts/agentic-coding-risks
  - topics/ai-software-development
status: complete
---

# Spec-Driven Development

**Domain**: AI-Assisted Software Engineering / Methodology

**One-line definition**: An approach to AI-assisted coding where a structured specification is written *before* prompting the AI — the spec becomes the source of truth that drives implementation rather than ad hoc prompting ("vibe coding").

---

## Definition

Spec-Driven Development (SDD) emerged as a structured response to the chaos of unconstrained AI code generation. The core principle: instead of describing what you want in a chat message and hoping for the best, you write an explicit, structured document (the "spec") that captures intent, constraints, and design decisions. The AI then implements against this spec.

**GitHub's framing**:
> "We're moving from 'code is the source of truth' to 'intent is the source of truth.' With AI, the specification becomes the source of truth and determines what gets built."

**Tessl's framing**:
> "A development approach where specs — not code — are the primary artifact. Specs describe intent in structured, testable language, and agents generate code to match them."

---

## Three Levels of SDD

Birgitta Böckeler (Thoughtworks) identifies three levels of commitment — each builds on the previous:

| Level | Description | Spec lifecycle |
|---|---|---|
| **Spec-first** | Write a spec before the AI session; use it to guide implementation; discard after | Created per task, then deleted |
| **Spec-anchored** | Keep the spec after the task and maintain it as the feature evolves | Lives alongside the code long-term |
| **Spec-as-source** | The spec *is* the primary artifact; humans only edit the spec, never the generated code | Code is marked "GENERATED FROM SPEC — DO NOT EDIT" |

Most practitioners operate at **spec-first** but aspire toward spec-anchored. Spec-as-source (implemented by Tessl) is the most ambitious and the least proven in practice.

---

## The Four-Phase Workflow (GitHub Spec Kit)

GitHub's **Spec Kit** implements the most widely-adopted SDD workflow:

1. **Specify**: Describe what you're building and *why* — user journeys, outcomes, success criteria. No technical details yet.
2. **Plan**: Provide your tech stack, architectural constraints, compliance requirements. AI generates a technical plan.
3. **Tasks**: AI breaks the spec + plan into small, independently implementable and testable chunks.
4. **Implement**: AI executes tasks one by one. Developer reviews focused, bounded changes.

**Key principle**: At each phase, the human *verifies and refines* — not just steers.

---

## REASONS Canvas (SPDD)

Wei Zhang and Jessie Jie Xia (Thoughtworks) extend SDD via **Structured Prompt-Driven Development (SPDD)**, treating prompts as versioned, reviewable team assets. Their **REASONS Canvas**:

| Component | Purpose |
|---|---|
| **R** — Requirements | What problem to solve; Definition of Done |
| **E** — Entities | Domain entities and relationships |
| **A** — Approach | Strategy for meeting requirements |
| **S** — Structure | Where the change fits; components and dependencies |
| **O** — Operations | Concrete, testable implementation steps |
| **N** — Norms | Cross-cutting engineering standards (naming, observability) |
| **S** — Safeguards | Non-negotiable boundaries (invariants, security rules) |

SPDD's key rule: **"When reality diverges, fix the prompt first — then update the code."**

---

## Tool Landscape

| Tool | Level | Workflow |
|---|---|---|
| **Kiro** (AWS) | Spec-first | Requirements → Design → Tasks; per-task markdown docs |
| **Spec Kit** (GitHub) | Spec-first / aspires spec-anchored | Constitution → Specify → Plan → Tasks |
| **Tessl** | Spec-as-source | 1:1 spec-to-file mapping; bidirectional sync |
| **SPDD / openspdd** | Spec-anchored | REASONS Canvas; versioned prompts; `/spdd-sync` |

---

## Spec vs. Memory Bank

A spec is distinct from the codebase-wide context files:

- **Memory bank / AGENTS.md**: Persistent, always-relevant rules and conventions. Applies to every session.
- **Spec**: Task-specific. Describes what to build *for this change*. May or may not persist after the task.

---

## Key Debates

**Problem size mismatch**: Both Kiro and Spec Kit work well for medium features. For small bugs, the workflow is overhead. For large, unclear problems, more specialist product input is needed than SDD provides.

**Review overload**: Spec Kit generates many markdown files. Böckeler: "I'd rather review code than all these markdown files." More documentation isn't automatically more control.

**MDD parallel**: Spec-as-source echoes 1990s Model-Driven Development — specs that generated code. MDD failed for business applications due to abstraction overhead. Böckeler warns spec-as-source may combine "the downsides of both MDD and LLMs: inflexibility *and* non-determinism."

**What works**: Spec-first consistently delivers on upfront clarity. Böckeler's observation: "Just because context windows are larger doesn't mean the AI properly picks up on everything in them."

---

## Related Pages

- [[concepts/agentic-development-loop]] — the implementation layer; SDD provides the what, the loop provides the how
- [[concepts/harness-engineering]] — quality harness complements SDD; feedforward guides and feedback sensors surround implementation
- [[concepts/agentic-coding-risks]] — SDD directly addresses Zechner's critique of unconstrained agent autonomy
- [[topics/ai-software-development]]

---

## Sources

- [[summaries/understanding-sdd-kiro-spec-kit-tessl--summary]] — Böckeler/Thoughtworks; three levels; Kiro, Spec Kit, Tessl
- [[summaries/spec-driven-development-spec-kit--summary]] — GitHub/Delimarsky; four-phase workflow
- [[summaries/spdd-structured-prompt-summary]] — Zhang & Xia/Thoughtworks; REASONS Canvas
- [[summaries/using-sdd-with-claude-code--summary]] — Heeki Park; practitioner experience
