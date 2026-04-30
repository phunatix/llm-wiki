---
title: "Using Spec-Driven Development with Claude Code — Summary"
type: summary
source_count: 1
created: 2026-04-29
last_updated: 2026-04-29
tags: [spec-driven-development, claude-code, practitioner-account, aws, developer-workflow]
inbound_links: 0
status: complete
source_file: "raw/inbox/Using spec-driven development with Claude Code.md"
related_pages: ["[[concepts/spec-driven-development]]", "[[concepts/agentic-development-loop]]", "[[topics/ai-software-development]]"]
---

**Author**: Heeki Park | **Published**: March 1, 2026 | **Source**: [heeki.medium.com](https://heeki.medium.com/using-spec-driven-development-with-claude-code-4a1ebe5d9f29)

A solutions architect's practitioner account of building an AWS AgentCore Gateway interceptor prototype using spec-driven development with Claude Code, operating in a posture that is mostly spec-first in practice but tends toward spec-anchored with deliberate effort. The most consequential observation is the "spec-once failure mode": SDD naturally begins as spec-first, and without active discipline it becomes spec-once — the spec is written upfront and then abandoned as implementation proceeds; distinguishing spec-first from spec-once requires the practitioner to continuously revisit and update the spec rather than treating it as a completed artifact. Five operational patterns are identified as high-value: upfront planning significantly reduces the proportion of follow-up interactions that require wholesale course corrections (earlier projects without it required constant replanning); stepwise builds with clear phases and modular stacks improve testability and isolate failures; instructing Claude Code to offer selectable option menus in clarifying questions accelerates back-and-forth; model selection matters practically — heavy Opus 4.6 use hit sliding window limits within 45–60 minutes, while Sonnet 4.6 sustained hours of continuous work; and parallel tmux sessions enable agent team patterns where multiple Claude Code instances work concurrently. A security lesson surfaces from the implementation: adding OAuth and authentication layers early is not optional, because changing `AuthorizerType` in AWS requires full stack replacement — a painful operation in enterprise pipelines that compounds if deferred. The project concluded with updates to both CLAUDE.md and a newly created SKILL.md, with custom skills identified as a significant accelerator for future work in the same domain.

## Key Insights

- The spec-once failure mode is the most practically useful concept in the piece: the difference between spec-first and spec-once is not structural but disciplinary — it requires the practitioner to return to the spec throughout implementation, not just at the start.
- Upfront planning has measurable follow-on effects: most subsequent interactions in the planned project were small tweaks; earlier unplanned projects required constant wholesale replanning. This is consistent with the four-phase Spec Kit model but grounded in direct comparison.
- Model selection is a practical operational concern, not just a quality concern: Opus 4.6 hits sliding window limits in 45–60 minutes of heavy use; Sonnet 4.6 does not. For sustained agentic sessions, model endurance is a real variable.
- The parallel tmux sessions pattern is the practitioner-level implementation of the agent team concept: multiple Claude Code instances running concurrently, each with defined scope, coordinated by the human on the loop.
- Security architecture decisions made late (auth layer, `AuthorizerType`) have disproportionate remediation costs in cloud infrastructure: what is a config change in code becomes a full stack replacement in AWS. The spec and plan phases are the right time to encode these constraints.
- CLAUDE.md and SKILL.md as project artifacts — updated and created as outputs of the engagement — represent the on-the-loop posture applied to tooling: the harness improves as a result of the session, not just the code.
- Cross-reference with Böckeler's critical taxonomy (`[[summaries/understanding-sdd-kiro-spec-kit-tessl--summary]]`): Park's account illustrates spec-first usage with aspiration toward spec-anchored, matching Böckeler's observation that most real-world SDD usage sits at the spec-first level regardless of tool claims.

## Related Pages

- [[concepts/spec-driven-development]]
- [[concepts/agentic-development-loop]]
- [[topics/ai-software-development]]
