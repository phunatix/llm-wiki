---
title: Agentic Coding Risks
type: concept
source_count: 1
created: 2026-04-13
last_updated: 2026-04-13
tags: [ai, coding-agents, software-quality, risk]
inbound_links: 0
status: complete
related_pages: ["[[concepts/ai-developer-stages]]", "[[topics/ai-software-development]]"]
---

# Agentic Coding Risks

**Domain**: AI & Software Development

**One-line definition**: The compounding, systemic risks that emerge when AI coding agents are used without sufficient human oversight — leading to unmaintainable codebases, cascading errors, and loss of architectural control.

## The Core Problem

Coding agents produce code fast. But they are not humans:
- They **don't learn** from repeated mistakes — the same booboos recur indefinitely
- They have **no bottleneck** — they can introduce errors at a rate humans cannot
- They have **local context only** — they never see the full codebase or all prior decisions
- They have **low recall** — the bigger the codebase, the worse their ability to find relevant existing code

A human making errors at high frequency is still rate-limited by human speed. An orchestrated army of agents has no such limit — errors compound at an unsustainable rate.

## The "Compounding Booboos" Failure Mode

Small coding errors (code smells, duplication, inconsistent abstractions) are harmless in isolation. But agents:
1. Introduce them at high velocity
2. Cannot observe the cumulative damage
3. Have no pain response that would trigger cleanup

Result: Weeks into an agentic project, the codebase has reached enterprise-level complexity — but in a team of 2 humans with no organizational muscle memory for it.

## The "Merchants of Complexity" Problem

Agents were trained on codebases that contain bad architectural decisions. When asked to architect a system, they produce:
- Immense amounts of code duplication
- Abstractions for abstraction's sake
- Cargo-cult "industry best practices"

Because agents never see each other's runs or the full history of decisions, every agent's decision is local — leading to systemic inconsistency.

## The "Agentic Search Has Low Recall" Problem

When the codebase becomes large, the agent cannot reliably find all relevant code before making changes. This causes:
- Code duplication (agent didn't find the existing implementation)
- Inconsistencies (agent made a local decision that conflicts with existing patterns)
- Incorrect refactors (agent missed files that needed updating)

The bigger the codebase, the worse this gets — making agents structurally unsuited to maintaining large, complex systems without tight human oversight.

## What Good Agent Tasks Look Like

Safe to delegate:
- Scoped tasks (agent doesn't need full system understanding)
- Self-evaluable (agent can measure its own output)
- Non-critical (failure is recoverable)
- "Rubber duck" / brainstorming (compress internet wisdom against your idea)

Dangerous to delegate:
- Architecture decisions
- API design
- Anything requiring full-codebase context
- Production-critical code without human review

## The Prescription

> "Slowing the fuck down is the way to go. Give yourself time to think about what you're actually building and why."

- Set limits on code generated per day, in line with your ability to review
- Write architecture and API by hand — the act of writing introduces useful friction
- Keep yourself in the loop; understanding the system enables you to fix it when something goes wrong

## Contradictions

- [[concepts/ai-developer-stages]] (Dohmke) presents a more optimistic view of full agentic delegation (Stage 4 "AI Strategist")
- The actual evidence from production (AWS alleged AI outage, Microsoft quality concerns, anecdotal "coded into a corner" reports) supports the more cautionary view

## See Also

- [[concepts/ai-developer-stages]]
- [[topics/ai-software-development]]

## Sources

- [[summaries/thoughts-on-slowing-down--summary]]
