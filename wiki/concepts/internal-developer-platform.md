---
title: Internal Developer Platform (IDP)
type: concept
source_count: 2
created: 2026-04-13
last_updated: 2026-04-13
tags: [platform-engineering, devops, developer-experience]
inbound_links: 0
status: complete
related_pages: ["[[concepts/golden-paths]]", "[[concepts/cognitive-load]]", "[[concepts/developer-self-service]]", "[[entities/Humanitec]]"]
---

# Internal Developer Platform (IDP)

**Domain**: Platform Engineering

**One-line definition**: A self-service layer that enables developers to provision infrastructure, deploy services, and manage their applications without direct dependence on an operations team.

## Definition

An IDP is the technical artifact that platform teams build and maintain to enable developer self-service. It abstracts infrastructure complexity via golden paths, exposes the right amount of cognitive load per team, and allows developers to "you build it, you run it" without requiring Kubernetes expertise for every service.

The term was coined by [[entities/Kaspar-von-Grunberg]] of [[entities/Humanitec]].

## What a Good IDP Provides

- Self-service deployment (developers can ship without ops involvement for standard cases)
- Visibility into what's running (logs, metrics, status)
- Opinionated defaults (golden paths) with the ability to escape to low-level when needed
- Consistent environments (dev / staging / production parity)
- Security and compliance guardrails baked in

## Common IDP Components

- **Platform Orchestrator**: Defines golden paths and abstracts infrastructure (e.g., Humanitec Platform Orchestrator)
- **Internal Catalog**: Service registry, documentation, templates (e.g., [[entities/Backstage]])
- **CI/CD**: Automated build and deployment pipelines
- **Monitoring**: Observability for developer-deployed services
- **Self-service portal**: UI or CLI for provisioning resources

## Key Statistic

By 2026, Gartner predicts 80% of software engineering organizations will have started a platform team or IDP initiative.

## Failure Modes

See [[concepts/cognitive-load]] for the two main failure modes:
1. Too much exposure → cognitive overload
2. Too much abstraction → golden cage / black box

## Common Pitfalls

- **Building for fashion, not need**: IDPs built because the category is fashionable — not because teams are clearly blocked — waste significant investment without delivering value
- **Ignoring culture**: Platform success depends heavily on communication, feedback loops, and iterative user engagement rather than on technology alone; an organizationally unsupported IDP stalls regardless of technical quality
- **Stopping at scaffolding**: Over-investing in new-service creation (Day 1) while leaving Day 2–50 operations (rollbacks, config changes, debugging) friction-heavy — see [[concepts/golden-paths]] for the prioritization framework

## See Also

- [[concepts/golden-paths]]
- [[concepts/cognitive-load]]
- [[concepts/developer-self-service]]
- [[entities/Humanitec]]
- [[entities/Backstage]]
- [[topics/platform-engineering]]

## Real-World Example: Zalando's Sunrise

Zalando built "Sunrise" on Backstage starting 2021: replaced 100+ disconnected interfaces, scaled to 40,000+ entities managed by a 4-engineer team, with 30 plugins covering 27 tools. The single most impactful adoption lever: **completely shut down old tooling** rather than hoping users would migrate voluntarily. See [[summaries/zalando-sunrise-backstage-summary]].

## Sources

- [[summaries/dark-side-of-self-service--summary]]
- [[summaries/whats-the-future-of-platform-engineering--summary]]
- [[summaries/zalando-sunrise-backstage-summary]] — Real-world Backstage IDP at 40k+ entity scale; adoption tactics
- [[sources/building-multi-tenant-kubernetes-on-azure-aks]] — Practical IDP concerns in shared Kubernetes clusters; tenancy boundaries and governance
