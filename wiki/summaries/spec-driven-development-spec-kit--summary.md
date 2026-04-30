---
title: "Spec-Driven Development with AI: Get Started with a New Open Source Toolkit — Summary"
type: summary
source_count: 1
created: 2026-04-29
last_updated: 2026-04-29
tags: [spec-driven-development, coding-agents, github, specifications, developer-workflow]
inbound_links: 0
status: complete
source_file: "raw/inbox/Spec-driven development with AI Get started with a new open source toolkit.md"
related_pages: ["[[concepts/spec-driven-development]]", "[[concepts/harness-engineering]]", "[[topics/ai-software-development]]"]
---

**Author**: Den Delimarsky (GitHub) | **Published**: September 2, 2025 | **Source**: [github.blog](https://github.blog/ai-and-ml/generative-ai/spec-driven-development-with-ai-get-started-with-a-new-open-source-toolkit/)

GitHub's Spec Kit is an open-source CLI toolkit built on the premise that coding agents should be treated as literal-minded pair programmers who require unambiguous instructions, not contextual inference. The article argues for a reorientation in how development artifacts are understood: specs are not static upfront documents but living, executable artifacts that evolve with the project, and the field is shifting from "code is the source of truth" to "intent is the source of truth." The toolkit enforces a four-phase workflow — Specify (high-level description of what and why, expressed as user journeys and outcomes, from which the agent generates a detailed spec); Plan (developer provides stack, architecture, and constraints, agent generates a technical plan drawing on internal docs, with multiple variants possible); Tasks (agent decomposes the spec and plan into small, independently testable chunks — concrete enough that each task has a clear acceptance criterion); and Implement (agent executes tasks one at a time, developer reviews focused changes rather than thousand-line dumps). Throughout, the human role is framed as verification at each checkpoint, not steering at each line. The article identifies three use cases where the approach is especially effective: greenfield projects (prevents generic boilerplate), feature work in existing systems (architectural constraints encode naturally into specs), and legacy modernization (captures intent while enabling fresh architecture). For large organizations, the spec and plan phases become the natural location to embed security policies, compliance rules, and design system constraints — making governance machine-readable instead of buried in wikis that neither humans nor agents reliably consult.

## Key Insights

- The core insight is a reframing of what a spec is: not a document for humans to hand off to developers, but a living artifact that governs agent behavior across the full feature lifetime — "not static documents but living, executable artifacts."
- The four-phase breakdown (Specify → Plan → Tasks → Implement) is a practical operationalization of the on-the-loop posture described in `[[concepts/harness-engineering]]`: the harness is the spec, plan, and task decomposition; the agent executes within it.
- Granularity of task decomposition is load-bearing: "create a user registration endpoint that validates email format" is a valid task; "build authentication" is not. The difference is testability and scope, not just size.
- Organizational governance becomes a first-class concern: security policies, compliance rules, and design system constraints belong in the spec and plan phases, where agents can actually act on them, rather than in documentation that is consulted inconsistently.
- Human verification — not just steering — is the framing for the developer's role: at each checkpoint, the developer confirms that the agent's output matches intent before proceeding, not that they approve of each implementation detail.
- The Spec Kit approach tends toward spec-anchored (spec kept for feature lifetime) rather than spec-first (spec as single-use prompt); this distinction is explored more critically in the Böckeler analysis (`[[summaries/understanding-sdd-kiro-spec-kit-tessl--summary]]`).

## Related Pages

- [[concepts/spec-driven-development]]
- [[concepts/harness-engineering]]
- [[topics/ai-software-development]]
