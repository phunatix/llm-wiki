---
title: Golden Paths
type: concept
source_count: 7
created: 2026-04-13
last_updated: 2026-04-23
tags:
  - concept
  - platform-engineering
  - developer-experience
  - devops
  - internal-developer-platform
related_pages:
  - concepts/cognitive-load
  - concepts/developer-self-service
  - concepts/internal-developer-platform
  - entities/Humanitec
  - entities/Kaspar-von-Grunberg
  - topics/platform-engineering
status: complete
---

# Golden Paths

**Domain**: Platform Engineering / Developer Experience

**One-line definition**: The opinionated, well-supported route through an organization's developer tooling that makes common tasks low-friction — the correct alternative to both "no standards" (fragmentation) and "golden cages" (mandated opaque abstractions).

---

## Origin

Coined at **Spotify** around 2014, in a Hack Week project for backend engineering. The team named it after the *Dune* concept: in Frank Herbert's *Children of Dune*, Paul Atreides sees a single path to human survival through countless futures and names it "The Golden Path." The platform team's framing was similar: one well-lit recommended route amid many possible paths, chosen deliberately for its long-term advantages.

From the original internal blog post:
> "This is the way we support an easy and streamlined way of working. If you are an adventurer you can of course leave the Golden Path and do your own thing, but then you will not have the same support."

Spotify had been operating with what they called **"rumour-driven development"**: the only way to learn how to do something was to ask a colleague. As they scaled, this became a bottleneck. Golden Paths were the answer — not by removing autonomy, but by making the recommended way discoverable and trusted.

---

## Definitions

Different practitioners have defined golden paths slightly differently, each emphasizing a useful angle:

| Source | Definition |
|---|---|
| **Spotify** (Niemen) | "The opinionated and supported path to build something" — tutorials guide developers through the recommended path for their engineering discipline |
| **Kaspar von Grünberg** (Humanitec CEO) | "Any procedure in the software development life cycle that a user can follow with minimal cognitive load and that drives standardization" |
| **Mallory Haigh** (platformengineering.org) | "A preconfigured, paved road that provides an end-to-end workflow for developers, enabled via an IDP" |

The common thread: reduce cognitive load by curating the path, while leaving the path escapable.

---

## The Golden Cage Anti-Pattern

A **golden cage** is what happens when a golden path goes wrong. Key failure modes:
- **Opaque**: Developers don't understand what the path does under the hood
- **Inescapable**: No mechanism to go off-path when needed; edge cases have no solution
- **Mandated**: Teams use it because they must, not because it's better
- **Stops at Day 1**: Works for new service creation but breaks for ongoing operations

The golden cage is a brittle abstraction that creates dependency without providing proportional value. Developer trust collapses when edge cases hit the wall.

> "Like any product, the real measure of a successful platform isn't adoption, but whether developers would choose your platform even if they weren't required to." — Bryan Ross

---

## Why Golden Paths Matter (Five Reasons)

1. **Reduced cognitive load**: Developers are freed from managing infrastructure, deployments, and security configurations. They focus on writing code.
2. **Improved consistency and reliability**: Standardized workflows reduce human error. Uniform processes are easier to troubleshoot and maintain.
3. **Faster development cycles**: Self-service capabilities eliminate wait times for ops team approvals. Developers move on their own timeline.
4. **Enhanced security and compliance**: Security best practices are baked into the path, not bolted on as a post-audit step.
5. **Developer satisfaction**: Reduced operational frustration leads to more engaged, productive engineers.

---

## Day 1 vs. Day 2–50: The Prioritization Mistake

Most platform teams optimize golden paths for **Day 1** — service creation, scaffolding, initial provisioning. This is a trap.

As Kaspar von Grünberg notes, the application creation process is **below 1% of the total time** invested in an application across its lifetime. Day 1 paths have small ROI.

**The prioritization framework** (von Grünberg, ~2022): rank potential golden paths by `frequency × (dev time + ops time)` to find the highest-leverage opportunities.

Example prioritization table (based on 100 deployments):

| Procedure | Frequency | Dev time (hrs) | Ops time (hrs) |
|---|---|---|---|
| Waiting for other teams | 6.3% | 16 | 16 |
| Debugging / error tracing | 4.4% | 10 | 10 |
| Add/update app configurations | 5% | 1 | 1 |
| Roll back failed deployment | 1.75% | 10 | 20 |
| Onboarding / retrain / swap teams | 1% | 80 | 16 |
| Add services and dependencies | 1% | 16 | 8 |

Focusing on **Day 2–50** — the ongoing operations phase — consistently produces higher ROI than optimizing onboarding flows.

> "Good golden paths turn every day into Day 1" — every day becomes a fresh starting point for optimization.

---

## Guardrails over Gates

The key framework from Bryan Ross (2025), backed by Matt Asay's AI-focused extension:

**The core question**: What genuinely must be universal, and what can be flexible?

**Gates** block developers who don't conform to the one true platform. They create adversarial dynamics, push workarounds underground, and reduce visibility.

**Guardrails** define boundary conditions, not implementation. They specify *outcomes* ("all production deployments must pass security baseline") not *methods* ("you must use tool X").

**Real example**: A large financial services firm reduced mandatory platform requirements to three non-negotiables:
1. All production deployments must pass the security baseline
2. All services must emit standardized metrics to the observability platform
3. All secrets must be retrieved from the secrets management system at runtime

Everything else became flexible. **Adoption went from 17% to 86% in six months** — and the platform team's relationship with developers shifted from adversarial to collaborative.

The principle: standardization through attraction, not through control.

> "Every forced choice should have a clear answer to 'what organisational risk does allowing flexibility here create?'" — Bryan Ross

---

## Components over Completeness

Companion principle to guardrails over gates:

**Platform teams** think in terms of "the platform" — a cohesive system teams either adopt wholesale or don't.  
**Developers** think in terms of "capabilities I need right now."

The solution: **platform-as-product with composable building blocks**. Expose capabilities (security scanning, deployment automation, secrets retrieval) as services that teams can integrate into their own workflows. Offer a complete example; don't mandate it.

Teams can adopt incrementally:
- A new team adopts everything
- A legacy team adapts specific components to meet guardrail requirements

The guardrails are universal; the implementation is composable. The more of the platform a team adopts, the less undifferentiated heavy lifting they do themselves — this is the "path of least resistance" dynamic that drives voluntary adoption.

---

## Exception Handling by Design

No guardrail system handles all real-world edge cases gracefully. The worst outcome is forcing teams to break out of the platform entirely when they hit these cases.

**Build exceptions into the platform**:
- An override flag (e.g., `override_security_scan`) with a required justification field
- Deployment proceeds, but triggers notification + audit log
- Weekly review of overrides — the pattern analysis reveals where guardrails need adjustment

This is "trust, but verify": teams can deviate when genuinely necessary, but the deviation is visible, documented, and used to improve the system.

---

## Dynamic Configuration Management

The root cause of most Day 2–50 pain is **static configuration management**: deployment pipelines that only work when the application's infrastructure doesn't change. Manual config updates, environment drift, and ops bottlenecks all flow from static configs.

**Dynamic Configuration Management (DCM)** (Humanitec): developers write workload specifications describing what their workload needs; the platform orchestrator dynamically generates the configuration for the target environment.

**RMCD pattern** (Humanitec Platform Orchestrator + Score):
1. **Read**: interpret workload spec and context
2. **Match**: find correct config templates and resource definitions
3. **Create**: generate environment-specific configurations
4. **Deploy**: deploy the workload wired to its dependencies

Benefits:
- Developers don't maintain environment-specific configs
- Updating a shared resource (e.g., Postgres version) propagates automatically across all dependent workloads
- Teams can extend the resource catalog (add a new database type) without ops intervention
- Standardization by design: every `git push` enforces organization-wide standards

See also: [[entities/Humanitec]]

---

## Golden Paths for AI

Matt Asay's 2025 extension of the guardrails-over-gates framing to AI adoption:

**The AI velocity gap**: developers are adopting AI tools faster than platform teams can standardize. Shadow AI (personal credit cards, unsecured APIs) is the shadow IT of 2025.

**The wrong response**: build a monolithic "official enterprise AI platform" over 18 months — it will be obsolete by launch. AI models are moving targets; committees can't approve what they don't yet understand.

**The right response** — composable AI guardrails:
1. **Interface standard**: OpenAI-compatible API as a de facto contract; backend-agnostic (allows model swaps without rewriting)
2. **API gateway**: enforcement and observability point; structured JSON outputs as standard; OpenTelemetry genAI conventions for cost/latency/token tracking
3. **Data governance**: runtime secret retrieval (no embedded keys); unified IAM
4. **Exits with obligations**: proceed-with-justification flag; extra logging, security review, tighter budgets for off-path AI use

The cognitive load of model selection, prompt engineering, retrieval patterns, and cost management is high. The platform's job is to lower it — letting the best developers move fast while protecting the enterprise from worst-case surprises.

---

## Success Factors (Spotify's Model)

Spotify's Golden Path tutorials are their most-read internal documentation and the cornerstone of new engineer onboarding. What made them work:

1. **Clearly defined audience**: Written for new engineers; this ensures clarity for everyone
2. **One main purpose**: "The opinionated and supported path to build your system" — not a how-to, not a reference, not education generically, but the *specific* path
3. **Step-by-step-by-step**: Every click, every command, every step — even when tedious. Missing steps cause confusion.
4. **True to the path**: When tooling changes (e.g., adopting Kubernetes), tutorials update simultaneously. Tutorial length is a diagnostic: long tutorials mean a long golden path, which is the real problem to fix.
5. **One per engineering discipline**: Backend, client, data engineering, data science, ML, web, audio processing
6. **Educational**: Even as paths get simpler, tutorials explain what's under the hood — understanding matters for long-term system health
7. **Special status**: Tutorials are the highest-priority documentation; owners are expected to prioritize them
8. **Feedback and testing**: New engineers run through the tutorials during onboarding — constant testing and feedback

---

## Golden State

Spotify concept: a **Golden State** is a list of compliance checks that verify whether a service is following the Golden Path. Ambition: get the entire engineering organization to pass Golden State checks, automatically identifying and upgrading systems that have drifted from the standard path. Reduces fragmentation and enables automatic upgrades across services using the same base configuration.

---

## Related Pages

- [[concepts/cognitive-load]] — the metric golden paths are designed to reduce
- [[concepts/developer-self-service]] — golden paths are the mechanism for good self-service
- [[concepts/internal-developer-platform]] — the technical implementation layer for golden paths
- [[entities/Humanitec]] — coined the IDP term; Platform Orchestrator enables DCM; Kaspar von Grünberg as key thought leader
- [[entities/Kaspar-von-Grunberg]] — Day 2–50 prioritization framework; DCM methodology
- [[topics/platform-engineering]] — broader context for golden path adoption

---

## Sources

- [[summaries/dark-side-of-self-service--summary]]: Primary source; golden paths vs. golden cages; 97% adoption stat
- [[summaries/whats-the-future-of-platform-engineering--summary]]: Cultural dimension of adoption
- [[summaries/golden-paths-what-are-they-summary]]: Definition, five reasons, design steps, examples (Haigh, 2025)
- [[summaries/spotify-golden-paths-summary]]: Origin story, Dune reference, success factors, Golden State (Niemen, Spotify)
- [[summaries/golden-paths-day-50-summary]]: Day 1 vs Day 2–50; prioritization table; DCM (Ransom/von Grünberg, 2023)
- [[summaries/golden-paths-one-size-summary]]: Guardrails over gates; 17%→86% adoption case study; composable platform (Ross, 2025)
- [[summaries/golden-path-to-ai-summary]]: AI velocity gap; composable AI guardrails; gateway pattern (Asay, 2025)
