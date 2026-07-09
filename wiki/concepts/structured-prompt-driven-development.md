---
title: Structured-Prompt-Driven Development (SPDD)
type: concept
source_count: 1
created: 2026-06-22
last_updated: 2026-06-22
tags: [ai-agents, coding-agents, prompts, software-engineering, thoughtworks]
inbound_links: 0
status: complete
related_pages: ["[[concepts/spec-driven-development]]", "[[concepts/harness-engineering]]", "[[concepts/agentic-coding-risks]]", "[[topics/ai-software-development]]"]
---

# Structured-Prompt-Driven Development (SPDD)

**Domain**: AI-Assisted Software Development / Engineering Method

**One-line definition**: An engineering method that treats structured prompts as first-class, version-controlled delivery artifacts — turning AI assistance from personal efficiency into a governed, team-level capability through the REASONS Canvas and a closed-loop prompt↔code synchronization workflow.

---

## The Problem It Addresses

AI coding assistants improve local speed (individual developer produces code faster), but that doesn't automatically translate into system-level throughput. When you look at the full delivery lifecycle:

- Ambiguous requirements become code quickly — **misunderstandings scale with speed**
- Reviews process more change — **inconsistency becomes easier to introduce**
- Integration/testing issues surface — **"generated" ≠ "aligned"**
- Production risk is harder to reason about when volume of change rises

> "It's like buying a Ferrari and driving it on muddy roads: the engine is powerful, but your arrival time is determined by road conditions and traffic."

SPDD asks: how do we make AI-generated changes **governable, reviewable, and reusable** so teams get faster *and* safer?

---

## The REASONS Canvas

A seven-part structure that guides a prompt from intent → design → execution → governance:

### Abstract Parts (Intent & Design)

| Dimension | Purpose |
|---|---|
| **R — Requirements** | What problem are we solving? What is Definition of Done? |
| **E — Entities** | Domain entities and their relationships |
| **A — Approach** | Strategy for meeting the requirements |
| **S — Structure** | Where the change fits in the system; components and dependencies |

### Specific Parts (Execution)

| Dimension | Purpose |
|---|---|
| **O — Operations** | Break strategy into concrete, testable implementation steps (down to method signatures) |

### Common Standards Parts (Governance)

| Dimension | Purpose |
|---|---|
| **N — Norms** | Cross-cutting engineering standards (naming, observability, defensive coding) |
| **S — Safeguards** | Non-negotiable boundaries (invariants, performance limits, security rules) |

The canvas aligns intent and boundaries **before** code is generated, moving uncertainty to the left. Reviewers reason about a single artifact instead of scattered chat logs and partial diffs.

---

## The SPDD Workflow

The workflow enforces a key rule: **when reality diverges, fix the prompt first — then update the code.**

```
Requirements → Analysis → REASONS Canvas → Code Generation → Verification → Release
     ↑                                            |
     |            Logic corrections:              |
     ←──── update prompt first, then code ────────┘
                                                  |
              Refactoring:                        |
     ←──── update code first, then sync prompt ──┘
```

### Closed Loop on Two Scales

**Within an iteration**: feedback flows back — logic corrections update the prompt before the code; refactoring syncs from code back to the prompt. Neither side silently diverges.

**Across iterations**: accumulated prompt assets (domain models, design decisions, norms) become the starting context for the next enhancement. Each cycle builds on a governed baseline.

---

## The openspdd CLI

Implements the SPDD workflow as repeatable commands:

| Command | Type | Purpose |
|---|---|---|
| `/spdd-story` | Optional | Breaks requirements into INVEST user stories |
| `/spdd-analysis` | Core | Extracts domain keywords, scans relevant code, produces strategic analysis |
| `/spdd-reasons-canvas` | Core | Generates full REASONS Canvas from analysis |
| `/spdd-generate` | Core | Generates code task-by-task following the Canvas strictly |
| `/spdd-api-test` | Optional | Generates cURL-based API test scripts |
| `/spdd-prompt-update` | Core | Updates Canvas when requirements change (requirements → prompt → code) |
| `/spdd-sync` | Core | Syncs code changes back into Canvas (code → prompt) |

---

## Three Core Skills

SPDD identifies three skills developers need in the AI era:

1. **Abstraction First** — Design before you generate. Know objects, collaborations, boundaries before the AI sprints on details.

2. **Alignment** — Lock intent before you write code. Make "what we will do / won't do" explicit; agree on standards and hard constraints up front.

3. **Iterative Review** — Turn output into a controlled loop. Not one-shot drafts, but an engineering process with review-and-iterate discipline.

---

## Relationship to Spec-Driven Development

SPDD is categorized as a **spec-anchored** approach in Böckeler's taxonomy (see [[concepts/spec-driven-development]]):
- It shares SDD's starting point: write the spec clearly first, then let the model implement
- It goes further: structured prompts are **governed, reusable, versioned team assets** that evolve alongside the code
- The prompt is not discarded after the task (spec-first) — it's maintained as the living record of design intent

Key difference from pure SDD: SPDD's closed-loop synchronization prevents the **spec-once failure mode** by design — the workflow forces prompt↔code alignment at every step.

---

## Fitness Assessment

| Rating | Scenario |
|---|---|
| ★★★★★ | Scaled, standardized delivery (many similar APIs, core workflows) |
| ★★★★★ | High compliance / hard constraints (financial, regulated) |
| ★★★★☆ | Team collaboration and auditability |
| ★★★★☆ | Cross-cutting consistency (multi-service refactors) |
| ★★☆☆☆ | Firefighting hotfixes |
| ★★☆☆☆ | Exploratory spikes |
| ★☆☆☆☆ | Poorly-defined domains / pure creative work |

---

## Key Ideas

- Prompts become **first-class delivery artifacts**: version-controlled, reviewed, reused, improved over time
- The REASONS Canvas moves uncertainty left — alignment before generation reduces rework
- Two types of post-generation changes: **logic corrections** (prompt first → code) vs. **refactoring** (code first → sync prompt)
- Individual expertise compounds across iterations as domain knowledge accumulates in prompt assets
- SPDD is most valuable where governability, traceability, and team consistency matter more than raw speed
- "In the AI era, software development isn't a contest of model IQ. It's a contest of engineer cognitive bandwidth."

---

## Open Questions

- How does SPDD scale to very large codebases with hundreds of accumulated prompt assets?
- Can the REASONS Canvas be auto-generated from existing specs/PRDs to reduce the "mindset shift" barrier?
- How should SPDD interact with existing CI/CD pipelines — should Canvas changes trigger builds?
- What's the learning curve for junior developers who haven't yet built the "abstraction first" muscle?

---

## Sources

- [[summaries/structured-prompt-driven-development--summary]] — Full method description; REASONS Canvas; billing engine example; three core skills; fitness assessment (Wei Zhang & Jessie Jie Xia, Thoughtworks/martinfowler.com, 2026)
