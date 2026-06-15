---
title: Harness Engineering
type: concept
source_count: 2
created: 2026-06-15
last_updated: 2026-06-15
tags:
  - concept
  - ai-software-development
  - coding-agents
  - quality
related_pages:
  - concepts/spec-driven-development
  - concepts/agentic-development-loop
  - concepts/agentic-coding-risks
  - topics/ai-software-development
status: complete
---

# Harness Engineering

**Domain**: AI-Assisted Software Engineering

**One-line definition**: The practice of building and maintaining the system of guides and sensors that surrounds a coding agent — controls that increase the probability of good output and provide feedback loops that self-correct before results reach human review.

---

## Definition

An agent's **harness** is everything except the model itself. The formula: **Agent = Model + Harness**. For coding agents specifically, the harness has two layers:

1. **Builder harness**: Built into the coding agent itself (system prompt, code retrieval, orchestration)
2. **User harness**: Built by the developer for their specific codebase and use case — rules files, tests, linters, review agents, etc.

**Harness Engineering** is the practice of building and iterating on the user harness. The goal: reduce review toil, increase system quality, and waste fewer tokens.

---

## Two Types of Controls

Every control in a harness is either **feedforward** (shapes what the agent produces) or **feedback** (evaluates what the agent produced and triggers correction). Controls are also either **computational** or **inferential**:

| | Computational | Inferential |
|---|---|---|
| **What** | Deterministic, CPU-run. Tests, linters, type checkers, structural analysis | Semantic analysis, AI code review, "LLM as judge" |
| **Speed** | Milliseconds to seconds | Seconds to minutes |
| **Cost** | Cheap | Expensive |
| **Reliability** | Deterministic | Non-deterministic |
| **Use for** | Every commit, every change | Selectively; higher-judgment problems |

**Examples**:
- Computational feedforward: language server (LSP), linters, code mods
- Computational feedback: type checker, test suite, ArchUnit boundary tests, dep-cruiser
- Inferential feedforward: AGENTS.md, skills, how-to guides
- Inferential feedback: AI code review agent, mutation testing analysis

---

## The Steering Loop

The human's role in harness engineering is to **steer**: iterate on the harness whenever issues recur. When an agent makes the same mistake twice, the response is not to fix the output — it's to fix the harness so the output improves automatically.

The steering loop can itself be AI-assisted: coding agents can write structural tests, generate draft rules from observed patterns, scaffold custom linters, or create how-to guides from codebase archaeology.

**The key discipline**: When something goes wrong, distinguish between fixing the artifact vs. fixing the harness. "In the loop" thinking fixes the artifact; "on the loop" thinking improves the harness.

---

## Three Harness Dimensions

### Maintainability Harness
Regulates internal code quality: duplicate code, cyclomatic complexity, missing test coverage, architectural drift, style violations. The most tractable harness type — mature tooling exists.

**What computational sensors catch reliably**: Structural duplication, coverage gaps, style violations, architectural drift.  
**What inferential sensors partially address**: Semantic duplication, brute-force fixes, over-engineered solutions.  
**What neither catches reliably**: Misdiagnosis of issues, overengineering, misunderstood instructions. These require human oversight.

### Architecture Fitness Harness
Guides and sensors that enforce architectural characteristics (fitness functions). Examples: performance requirements as feedforward + performance tests as feedback; observability standards as feedforward + log quality checks as feedback.

### Behaviour Harness
The hardest problem: does the application functionally behave as needed? Current state: most teams use AI-generated tests as their primary feedback, which "puts a lot of faith in AI-generated tests — that's not good enough yet." Approved fixtures patterns help selectively but aren't a wholesale answer.

---

## Timing: Keep Quality Left

Distribute checks across the delivery lifecycle by cost and speed:

- **Before/during coding**: Fast computational sensors (linters, type checkers, fast test suites). Should run alongside the agent.
- **Pre-commit / pre-push**: Heuristic-based linters, relevant test subsets.
- **Post-integration pipeline**: Slower, broader checks (mutation testing, architectural review agents, detailed AI review).
- **Continuous codebase monitoring**: Drift detection (dead code, dependency scanning, SLO degradation) running outside the change lifecycle.

---

## Harnessability

Not every codebase is equally amenable to harnessing:
- **Strongly typed languages**: Type checker is a free sensor
- **Clear module boundaries**: Architectural constraint rules are buildable
- **Frameworks with abstractions**: Reduce what the agent needs to know

**Greenfield teams** can bake harnessability in from day one. **Legacy teams** face a harder problem: the harness is most needed where it is hardest to build (high technical debt, weak typing, unclear boundaries).

---

## Harness Templates

Mature organizations codify common service topologies (API service, event processor, data dashboard) into **harness templates** — bundles of guides and sensors for a topology. Teams may choose tech stacks partly based on what harnesses are already available. Faces the same versioning and drift problems as service templates.

---

## Real-World Examples

- **OpenAI**: Layered architecture enforced by custom linters and structural tests; recurring "garbage collection" scans for drift. Conclusion: "Our most difficult challenges now center on designing environments, feedback loops, and control systems."
- **Stripe**: Pre-push hooks running relevant linters based on heuristics; "blueprints" integrating feedback sensors into agent workflows.
- **Thoughtworks**: "Janitor army" agents for code quality; API quality with custom linters + agents.

---

## Related Pages

- [[concepts/spec-driven-development]] — SDD provides feedforward context (the spec); harness engineering provides the surrounding quality controls
- [[concepts/agentic-development-loop]] — Kakkar's friction-removal loop; the harness is the infrastructure being built
- [[concepts/agentic-coding-risks]] — Doernenburg's internal quality analysis; harness is the response to the risks Zechner identifies

---

## Sources

- [[summaries/harness-engineering-for-coding-agents--summary]] — Full harness engineering framework; computational vs inferential; three regulation dimensions; harnessability
- [[summaries/assessing-internal-quality-with-agent--summary]] — Doernenburg/Thoughtworks; CCMenu case study; AI tendency to introduce technical debt; internal quality
