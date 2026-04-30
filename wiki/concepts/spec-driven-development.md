---
title: Spec-Driven Development (SDD)
type: concept
source_count: 4
created: 2026-04-29
last_updated: 2026-04-29
tags: [ai-agents, coding-agents, specifications, developer-workflow, software-engineering]
inbound_links: 0
status: complete
related_pages: ["[[concepts/harness-engineering]]", "[[concepts/agentic-coding-risks]]", "[[concepts/agentic-development-loop]]", "[[topics/ai-software-development]]"]
---

# Spec-Driven Development (SDD)

**Domain**: AI-Assisted Software Development / Engineering Practice

**One-line definition**: A development practice where structured, behavior-oriented specifications written in natural language precede code generation — specs serve as the shared source of truth between humans and AI agents, replacing vague prompts with precise intent.

---

## The Problem It Addresses

Vague prompting forces the AI to guess at thousands of unstated requirements. The model makes reasonable assumptions — some will be wrong, and you often won't discover which ones until deep into implementation. SDD replaces guess-work with precision: the agent knows *what* to build (spec), *how* to build it (plan), and *in what order* (tasks) before writing a line of code.

> "We treat coding agents like search engines when we should be treating them more like literal-minded pair programmers. They excel at pattern recognition but still need unambiguous instructions." — GitHub Spec Kit

---

## Three Levels of SDD

Not all "spec-driven" approaches are the same. Birgitta Böckeler (Thoughtworks) identifies a useful taxonomy:

| Level | Description | Spec lifecycle |
|---|---|---|
| **Spec-first** | A well-thought-out spec is written before coding, then used for the task at hand | Spec may be discarded after the task is complete |
| **Spec-anchored** | Spec is kept after the task and continues to serve as the reference for evolution and maintenance | Spec lives as long as the feature |
| **Spec-as-source** | The spec is the primary artifact; humans only edit the spec, never the code directly | Code is generated from spec; code files may be marked `// GENERATED — DO NOT EDIT` |

Most current tools implement spec-first only. Spec-anchored is the aspiration of some tools (GitHub Spec Kit says specs should be "living artifacts"). Spec-as-source is the most ambitious level — currently explored by Tessl, with direct parallels to 1990s model-driven development (MDD).

---

## The Spec-Once Failure Mode

The most common failure in practice: a thorough spec launches the project, but as implementation proceeds the spec is abandoned. The spec-once failure mode looks like spec-first but produces the worst outcome — the spec is neither maintained nor useful. The discipline of revisiting and updating the spec at each implementation step is what separates real SDD from spec-once.

---

## What Is a Spec?

A spec is a **structured, behavior-oriented artifact** written in natural language that expresses software functionality and serves as guidance to AI coding agents.

Useful distinction: **spec vs. memory bank**
- **Memory bank** (AGENTS.md, CLAUDE.md, architecture.md): persistent context relevant to *all* coding sessions in the codebase — project-wide conventions, stack description, coding standards
- **Spec**: task-specific — relevant only to the feature or change currently being built; scoped to a particular user journey or behavior

A spec is closer to a Product Requirements Document (PRD) than to a technical design. It should describe user journeys, outcomes, and what success looks like — not implementation choices (those belong in the plan phase).

---

## Four-Phase Workflow (Specify → Plan → Tasks → Implement)

*As defined by GitHub Spec Kit; variations exist across tools*

**1. Specify** — Provide a high-level description of *what* to build and *why*. Focus on user journeys, experiences, and outcomes. Who uses this? What problem does it solve? What does success look like? The agent fleshes out the details into a full specification. Result: a living artifact.

**2. Plan** — Provide the technical direction: stack, architecture, constraints, integration requirements, performance targets, compliance needs. The agent generates a comprehensive technical plan. Make internal architectural guidelines available here — the agent integrates your standards directly into the plan. Multiple plan variants can be generated for comparison.

**3. Tasks** — The agent breaks the spec + plan into small, reviewable, independently implementable chunks. Each task should be testable in isolation. Instead of "build authentication," you get "create a user registration endpoint that validates email format and returns a 400 with a structured error for invalid input."

**4. Implement** — The agent tackles tasks one by one (or in parallel where applicable). The developer reviews focused changes that solve specific problems — not thousand-line code dumps. The agent knows what to build (spec), how (plan), and what to work on (task).

**Crucial throughout**: your role is to verify, not just steer. At each phase, reflect and refine — does the spec capture what you actually want? Does the plan account for real-world constraints? Did the AI miss edge cases?

---

## Tool Landscape (as of late 2025)

| Tool | Level | Approach | Notes |
|---|---|---|---|
| **Kiro** (AWS) | Spec-first | Lightweight; Requirements → Design → Tasks; VS Code-based | Verbose for small problems; no clear spec-anchored path |
| **GitHub Spec Kit** | Spec-first (aspires to anchored) | CLI; constitution (memory bank) + slash commands; many files per spec | Most customizable; per-spec git branch suggests spec lifetime = change request |
| **Tessl** | Spec-anchored → spec-as-source | CLI + MCP server; 1:1 spec-to-code-file mapping; `tessl build` generates code | Still in beta; deepest SDD ambition; non-determinism a real concern |

---

## Critical View: The MDD Parallel

Böckeler draws an important historical comparison: **model-driven development (MDD)** in the 1990s-2000s used formal models (UML, custom DSLs) as the source of truth, with custom code generators producing the implementation. MDD never took off for business applications — it created an awkward abstraction level with significant overhead and constraints.

SDD with LLMs removes MDD's parseable-format constraint and eliminates custom code generators. But the trade-off: LLMs introduce non-determinism. The parseable structure of MDD provided tool support for validating spec completeness and consistency — something LLM-based specs lose.

The risk: spec-as-source and spec-anchored may end up with the downsides of *both* MDD (inflexibility) and LLMs (non-determinism). Early evidence — agents ignoring constitution articles, duplicating code the spec described as existing — suggests this is a real concern.

> "I wonder if some of them are trying to feed AI agents with our existing workflows too literally, ultimately amplifying existing challenges like review overload and hallucinations." — Birgitta Böckeler

---

## When SDD Works Well

1. **Greenfield** — Starting fresh; a small spec investment ensures the AI builds to intent, not to generic patterns
2. **Feature work in existing codebases** — Spec forces clarity on how a new feature interacts with existing systems; plan encodes architectural constraints; new code feels native rather than bolted-on
3. **Legacy modernization** — Original intent is captured in a modern spec; fresh architecture in the plan; AI rebuilds without carrying forward inherited technical debt

**Where SDD struggles**: Small bugs and changes (workflow overkill); large, unclear features (requires specialist product/requirements skills and stakeholder involvement before speccing); any situation where iterating on code is faster than iterating on spec.

---

## Practical Observations

From practitioner accounts:
- **Upfront planning pays dividends**: Most follow-up interactions become small tweaks rather than wholesale changes; mid-course correction frequency drops significantly
- **Build stepwise**: Combine SDD with stacked PRs — small, independently reviewable chunks match the task-level granularity SDD produces
- **Spec-once is the failure mode**: The discipline is in *continuously revisiting* the spec as the implementation evolves
- **One workflow does not fit all sizes**: Current tools are better suited to medium-complexity features than to small bugs or large unclear initiatives
- **Review fatigue**: Elaborate SDD tools generate many markdown files; some practitioners find it less taxing to review code than the spec artifacts

---

## Key Ideas

- SDD replaces "pattern-complete what I vaguely described" with "execute what I precisely specified" — agents need unambiguous instructions, not mind-reading
- Three levels (spec-first / anchored / as-source) are meaningfully different; most tools only implement spec-first despite aspirations otherwise
- The spec-once failure mode is the most common; discipline means revisiting the spec throughout
- The MDD parallel is a sobering historical lens: spec-as-source is ambitious and carries real risks of inflexibility combined with LLM non-determinism
- SDD is most powerful for feature work in existing codebases where intent must mesh with existing constraints

---

## Open Questions

- How should spec size/granularity vary with problem size? Current tools don't yet solve the "sledgehammer for a bug" problem
- How does a spec-anchored workflow stay manageable as specs multiply across a large codebase?
- Can inferential sensors (LLM evaluations) be used to verify spec completeness and consistency — recovering some of the tooling benefit MDD had?
- Will spec-as-source face the same adoption ceiling as MDD, or does LLM flexibility change the calculus fundamentally?

---

## Sources

- [[summaries/spec-driven-development-spec-kit--summary]] — GitHub Spec Kit; four-phase workflow; "intent is the source of truth"; three use cases (Den Delimarsky, GitHub, 2025)
- [[summaries/understanding-sdd-kiro-spec-kit-tessl--summary]] — Three levels of SDD; Kiro/Spec Kit/Tessl comparison; MDD parallel; critical observations (Birgitta Böckeler, Thoughtworks, 2025)
- [[summaries/using-sdd-with-claude-code--summary]] — Practitioner account; spec-once failure mode; upfront planning pays dividends; stepwise builds (Heeki Park, 2026)
- [[summaries/building-elite-ai-engineering-culture--summary]] — SDD as one of key practices in elite AI engineering orgs; Thoughtworks calling it "one of the most important practices of 2025" (cjroth.com, 2026)
