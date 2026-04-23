---
title: Agentic Infrastructure
type: concept
source_count: 1
created: 2026-04-10
last_updated: 2026-04-23
tags: [ai-agents, platform-engineering, automation, governance]
inbound_links: 0
status: complete
related_pages: ["[[concepts/golden-paths]]", "[[concepts/governance-by-default]]", "[[concepts/model-context-protocol]]", "[[concepts/agentic-development-loop]]", "[[topics/platform-engineering]]", "[[topics/ai-software-development]]"]
---

# Agentic Infrastructure

**Domain**: Platform Engineering / AI Agent Operations

**One-line definition**: The platform discipline of treating AI agents as first-class, governed actors inside delivery systems — giving them permissions, quotas, guardrails, and curated workflows rather than letting them operate as ungoverned scripts bolted onto existing pipelines.

---

## The Core Idea

Most organizations initially treat AI agents as tools individual developers use. Agentic infrastructure is the recognition that as agent autonomy increases — agents writing PRs, running tests, deploying services, managing infrastructure — they need to be governed like any other actor in the system.

The analogy: service accounts and RBAC didn't exist in early software systems. As automation grew, they became essential. AI agents are the next category of actor requiring the same treatment.

---

## What "First-Class" Means in Practice

| Human Developer | AI Agent (agentic infrastructure) |
|---|---|
| Access via SSO + MFA | Access via scoped service account / API key |
| RBAC governs what they can do | Agent role governs what tools/environments it can reach |
| Deploys via CI/CD pipeline | Deploys via approved agent workflow with audit log |
| Subject to cost allocation | Subject to compute/token budget with alerting |
| Follows golden path documentation | Follows **agent golden path** — approved tool sequences |

---

## Agent Golden Paths

The concept of [[concepts/golden-paths]] extends naturally to AI agents. An agent golden path defines:

- Which tools the agent is permitted to use (e.g., can read code, cannot push to main without review)
- Which environments the agent can operate in (dev yes, production no without approval)
- What the agent's "done" criteria look like (self-verification, test pass, human review gate)
- How deviations are logged and reviewed

This is the AI-era equivalent of developer golden paths: the approved, supported, observable way for agents to operate — not a constraint on what agents *can* do, but a guardrail around *how* they do it.

---

## Platform Responsibilities Expanding

Agentic infrastructure represents a broadening of the platform engineering mandate. Historically, platform teams governed:
- Infrastructure provisioning
- Deployment pipelines
- Service configuration

With AI agents in the delivery system, platform teams also govern:
- Agent authentication and scope
- Tool and resource registries (see [[concepts/model-context-protocol]])
- Budget and rate limits per agent
- Observability into agent actions (what was called, what changed, why)
- Approval gates for high-stakes agent actions

The platform becomes less a tool provider and more an **autonomous-change supervisor**.

---

## Connection to Governance by Default

[[concepts/governance-by-default]] is the design pattern that makes agentic infrastructure work: compliant, observable behavior becomes the default path, not an optional add-on. Policy-as-code, automatic control injection, and service templates mean agents operate within guardrails by design — even when those agents generate code or trigger deployments autonomously.

---

## Key Ideas

- Platforms should treat AI agents as governed personas, not as ad hoc scripts
- Agent golden paths extend the developer golden path concept to autonomous actors
- As agents become more autonomous, platform engineering shifts from tool exposure to supervised autonomous change
- The platform's job is to make the safe, observable path the easiest path for agents to follow

---

## Open Questions

- What technical controls are most realistic for agent governance: RBAC, compute budgets, approval gates, policy engines, or environment isolation?
- How different is agentic infrastructure from conventional CI/CD automation — is it a new category or an extension?
- When agents generate code that other agents then deploy, where does human oversight need to be inserted?

---

## Sources

- [[sources/10-platform-engineering-predictions-2026]] — "10 Platform Engineering Predictions for 2026"; agentic infrastructure as predicted platform evolution; agent golden paths; supervised autonomous change
