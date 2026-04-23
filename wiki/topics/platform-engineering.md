---
title: Platform Engineering
type: topic
source_count: 8
created: 2026-04-13
last_updated: 2026-04-23
tags: [devops, platform, developer-experience, idp, golden-paths]
inbound_links: 0
status: complete
related_pages: ["[[concepts/developer-self-service]]", "[[concepts/internal-developer-platform]]", "[[concepts/golden-paths]]", "[[concepts/cognitive-load]]", "[[concepts/forward-deployed-engineer]]", "[[entities/Humanitec]]"]
---

# Platform Engineering

**Scope**: The practice of designing, building, and maintaining internal developer platforms (IDPs) to improve developer productivity, reduce cognitive load, and enable self-service infrastructure.

**Overview**: Platform engineering emerged from DevOps as organizations recognized that "you build it, you run it" without proper tooling creates unsustainable cognitive load for developers. The discipline focuses on building opinionated, self-service platforms that abstract complexity without restricting developer freedom.

## What's Included

- Internal Developer Platforms (IDPs)
- Developer self-service tooling
- Golden paths and developer experience
- Cognitive load management
- Platform team structures and culture
- Forward-deployed platform engineers
- AI integration into platforms

## Core Concepts

- [[concepts/developer-self-service]]: The principle that developers should be able to provision and manage their own infrastructure
- [[concepts/internal-developer-platform]]: The technical artifact that enables self-service
- [[concepts/golden-paths]]: Opinionated default paths that abstract complexity without removing freedom
- [[concepts/cognitive-load]]: The key metric for evaluating self-service quality
- [[concepts/forward-deployed-engineer]]: Engineers embedded in teams to bridge platform and users

## Key Entities

- [[entities/Humanitec]]: Pioneer in IDP space; coined the term IDP; Platform Orchestrator product
- [[entities/Kaspar-von-Grunberg]]: CEO of Humanitec; coined "Internal Developer Platform"
- Google DORA: Research organization measuring DevOps performance; tracks platform engineering trends

## Key Debates

- **Self-service vs. over-abstraction**: Too much self-service overwhelms developers; too much abstraction creates "golden cages"
- **Build vs. buy**: Should you build your own IDP or use a product like Humanitec?
- **Culture vs. technology**: "10% technical, 90% cultural change" — the human side often fails even when tech succeeds
- **Gates vs. guardrails**: Mandated monolithic platforms vs. composable guardrails that attract rather than coerce (Ross 2025: 17%→86% adoption by reducing mandatory items to three)
- **Day 1 vs. Day 2–50**: Most platform teams over-invest in scaffolding/onboarding; ongoing operations (debugging, rollbacks, config changes) are <1% Day 1, 99% everything else
- **AI + platform engineering**: Will agentic AI make platform engineering obsolete, or will platforms need to support AI workloads (GPU orchestration, model serving, AI velocity gap)?

## Recent Developments

- **2025-2026**: Gartner predicts 80% of software engineering orgs will have a platform team by 2026
- **2025**: AI/agentic coding tools creating new demands on platforms (GPU orchestration, model serving)
- **2025**: DORA and Humanitec surveys show platform engineering "fledgling at best" — adoption issues persist
- **2025**: The platform engineering discipline is specializing into more focused sub-roles: DevEx engineering, platform security, observability engineering, AI enablement, and platform product management — reflecting that the "platform team" label now covers a broader surface than it did five years ago

## Key Insights

- Platform engineering is primarily a cultural problem, not a technical one
- 97% of developers follow a golden path once established, if they understand and trust it
- Division of labor is inevitable at scale — the question is where the handoff point is, not whether ops should exist
- Cognitive load is the right lens for evaluating self-service design
- Treating developers as users (with feedback loops, metrics, and iteration) is the highest-leverage principle
- Standardization through attraction beats standardization through control — the measure is whether developers would choose your platform even if not required
- Prioritize Day 2–50 golden paths: ongoing operations (rollbacks, config changes, debugging) consume 99% of application lifetime; service scaffolding is <1%
- Dynamic Configuration Management (DCM) resolves the root cause of most Day 2–50 friction: static configs that break when infrastructure changes

## See Also

- [[topics/ai-software-development]]: AI is both a challenge for and user of platform engineering
- [[topics/devops-homelab]]: Related DevOps practices
- [[concepts/sre-anything-framework]]: SRE principles that inform platform reliability thinking

## Sources by Relevance

- [[summaries/dark-side-of-self-service--summary]]: Core source on what not to do; the cognitive load model
- [[summaries/whats-the-future-of-platform-engineering--summary]]: Current state and AI intersection
- [[summaries/forward-deployed-engineer--summary]]: The FDE role as bridge between platform and users
- [[summaries/spotify-golden-paths-summary]]: Origin of golden paths; Dune reference; success factors; Golden State concept
- [[summaries/golden-paths-day-50-summary]]: Day 1 vs Day 2–50 prioritization; DCM as root-cause fix; frequency × time table
- [[summaries/golden-paths-one-size-summary]]: Guardrails over gates; 17%→86% adoption case study; composable platform design
- [[summaries/golden-path-to-ai-summary]]: AI velocity gap; composable AI guardrails; OpenAI-compatible API as interface standard
- [[summaries/golden-paths-what-are-they-summary]]: Foundational definition; five reasons; design methodology
