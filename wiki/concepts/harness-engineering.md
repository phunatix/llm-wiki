---
title: Harness Engineering
type: concept
source_count: 2
created: 2026-04-29
last_updated: 2026-04-29
tags: [ai-agents, coding-agents, developer-tooling, quality, feedback-loops, platform-engineering]
inbound_links: 0
status: complete
related_pages: ["[[concepts/agentic-coding-risks]]", "[[concepts/agentic-development-loop]]", "[[concepts/agentic-infrastructure]]", "[[concepts/governance-by-default]]", "[[concepts/spec-driven-development]]", "[[topics/ai-software-development]]"]
---

# Harness Engineering

**Domain**: AI-Assisted Software Development / Developer Tooling

**One-line definition**: The practice of building and maintaining a system of feedforward guides and feedback sensors that regulate what coding agents produce — shifting developer effort from reviewing every line of generated code to building the environment that makes agents self-regulate.

---

## The Problem It Solves

Coding agents generate code quickly. The output often compiles and passes superficial checks. But without deliberate controls, agents systematically introduce:
- Non-idiomatic code that works but violates the codebase's established conventions
- Unnecessary complexity (caches, abstraction layers) for problems that don't require it
- Duplication of existing utilities the agent didn't know about
- Type system violations that technically compile but lose semantic intent

The developer choice is then: review every line (bottleneck), or accept degraded quality silently (technical debt). Harness engineering is the third path: build the controls that make the agent catch its own problems.

---

## The Framework: Guides and Sensors

A harness has two components, borrowed from cybernetics (governor model):

### Feedforward Guides
Proactive context fed to the agent *before* it acts — shaping what it produces:
- AGENTS.md / CLAUDE.md — project conventions, coding standards, architectural rules
- Specs and task breakdowns — what to build and how
- Architecture descriptions — existing patterns the agent should follow
- Performance requirements — constraints embedded in the workflow

### Feedback Sensors
Reactive signals fed to the agent *after* it produces output — allowing it to evaluate and correct:
- **Computational sensors**: deterministic, cheap, fast. Linters, type checkers, test suites, code coverage, architectural drift detectors, complexity metrics. These catch structural problems reliably and at low cost.
- **Inferential sensors**: LLM-based evaluation. Can address semantic problems (duplicate logic, redundant tests, over-engineered solutions) that require judgment, but expensively and probabilistically — not on every commit.

The agent's workflow becomes a closed loop: produce → sense → correct → produce again.

---

## Three Harness Dimensions

Not all harness work has the same difficulty or tooling availability:

| Dimension | What it governs | Current state |
|---|---|---|
| **Maintainability** | Code quality, duplication, complexity, style, test coverage, architectural drift | Most tractable — rich pre-existing tooling; computational sensors cover most cases |
| **Architecture fitness** | Performance, observability standards, API quality, integration constraints | Tractable with fitness functions; mix of computational and inferential sensors |
| **Behavior** | Does the system do what users need? Does it function correctly? | Hardest — still largely dependent on AI-generated test suites (often inadequate) and human testing; open research problem |

The behavior harness is the elephant in the room. Computational and inferential sensors can't reliably catch misdiagnosis of the problem, over-engineering, or misunderstood instructions. The agent's test suite, even at high coverage, verifies what was built — not whether what was built is right.

---

## Humans: Outside / In / On the Loop

Three postures for humans in AI-assisted development (Kief Morris, Thoughtworks):

**Outside the loop** — Humans run the "why loop" (what to build), agents run the "how loop" (how to build it). The appeal: the why loop is what we actually care about. The risk: internal quality degrades silently; agents spiral when they hit complex problems; no mechanism to course-correct.

**In the loop** — Humans stay closely involved in the innermost code-generation loop, manually inspecting every line. The appeal: human judgment still exceeds agents in many edge cases. The problem: agents produce code faster than humans can inspect it; humans become the bottleneck.

**On the loop** — Humans build and maintain the harness, then let the agent run within it. Instead of fixing a bad artefact directly, you fix the harness that produced it — so the improvement applies to all future outputs. This is the sustainable model at scale.

> "The difference between in the loop and on the loop is most visible in what we do when we're not satisfied with what the agent produces. The 'in the loop' way is to fix the artefact. The 'on the loop' way is to change the harness that produced the artefact."
> — Kief Morris

---

## The Agentic Flywheel

The next level beyond "on the loop": humans direct agents to manage and improve the harness itself.

The flywheel works by:
1. Feeding agents the harness's own test results, evaluations, and performance signals
2. Having agents review workflow outputs and recommend harness improvements
3. Agents propose improvements to the backlog; humans prioritize
4. High-confidence improvements get automatically approved and applied

The result: a harness that generates recommendations for improving itself. Initially this requires human approval for each change; as confidence grows, the threshold for auto-approval can lower. At the extreme, this converges toward a self-improving system — but one that got there through engineered discipline, not vibe coding.

---

## Harnessability

Not every codebase is equally amenable to harnessing:

- **Strongly typed languages** give type-checking as a free sensor
- **Clear module boundaries** support architectural constraint rules
- **Frameworks that abstract detail** reduce what agents need to get right
- **Greenfield teams** can bake harnessability in from day one — technology and architecture choices determine how governable the system will be
- **Legacy codebases** face the harder problem: the harness is most needed where it is hardest to build (high technical debt, poor test coverage, monolithic structure)

---

## Harness Templates

In mature engineering organizations, common service topologies (REST API service, event processor, data dashboard) are already codified as service templates. These may evolve into **harness templates** — bundles of guides and sensors appropriate for a given topology, instantiated when a team picks a stack.

The same challenges apply: once teams instantiate a template, they diverge from upstream improvements. Harness templates face versioning and contribution problems, potentially worse than service templates because guides and sensors are harder to test than code.

---

## Connection to Platform Engineering

From a platform engineering perspective, harness engineering is the mechanism that makes [[concepts/agentic-infrastructure]] practical: rather than governing AI agents through access controls alone, the platform provides the guides (golden paths for agents) and sensors (compliance checks, quality gates) that make the right behavior automatic. [[concepts/governance-by-default]] is the design principle; harness engineering is the implementation discipline.

---

## Key Ideas

- Harness engineering shifts developer effort from artifact review to environment design — "on the loop" rather than "in the loop"
- Computational sensors (linters, type checkers, tests) are cheap and reliable for structural problems; inferential sensors (LLM-based) handle semantic problems expensively
- The behavior harness is the hardest and least solved dimension — agent-generated tests are necessary but not sufficient
- The agentic flywheel closes the loop: agents directed to improve their own harness produce self-improving systems
- Harnessability is a design property: greenfield teams should treat it as a first-class architectural concern

---

## Open Questions

- How do we keep a harness coherent as it grows — guides and sensors in sync, not contradicting each other?
- How far can we trust agents to make sensible trade-offs when instructions and feedback signals conflict?
- If sensors never fire, is that high quality or inadequate detection?
- What tooling helps configure, sync, and reason about a harness as a system rather than scattered controls?

---

## Sources

- [[summaries/harness-engineering-for-coding-agents--summary]] — Primary source; guides/sensors framework; three dimensions; computational vs inferential sensors; harness templates (Thoughtworks, 2026)
- [[summaries/humans-and-agents-software-loops--summary]] — Why/how loop model; outside/in/on the loop; the agentic flywheel (Kief Morris, Thoughtworks, 2026)
