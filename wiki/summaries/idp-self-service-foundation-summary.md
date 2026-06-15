---
title: "Summary: Design a Developer Self-Service Foundation (Microsoft)"
type: summary
source_count: 1
created: 2026-06-15
last_updated: 2026-06-15
tags: [summary, platform-engineering, internal-developer-platform, developer-self-service]
source_file: "raw/inbox/Design a Developer Self-Service Foundation.md"
related_pages:
  - concepts/developer-self-service
  - concepts/internal-developer-platform
  - entities/Humanitec
  - topics/platform-engineering
status: complete
---

# Summary: Design a Developer Self-Service Foundation (Microsoft)

**Source**: Microsoft Learn — "Design a Developer Self-Service Foundation"
**Author**: juliakm (Microsoft Platform Engineering)
**URL**: https://learn.microsoft.com/en-us/platform-engineering/developer-self-service
**Published**: (n.d.) | **Clipped**: 2026-06-15
**Type**: Technical reference / architecture guide

---

## Key Takeaways

**The two primary categories of self-service**: Automation (higher priority — reduces toil, ensures compliance, enables least-privilege without manual service desk) and Data Aggregation (useful but secondary; helps track automated requests and their results).

**The five foundational components of a developer self-service platform**:
1. **Developer Platform API**: Single point of contact for all UX; acts as authentication and security layer; system's contract with other systems
2. **Developer Platform Graph**: Managed data graph associating entities (environments, resources, APIs, repos, components) and templates from multiple providers
3. **Developer Platform Orchestrator**: Routes and tracks template-based requests; coordinates with task/workflow engines; provides abstraction over multiple CI/CD systems; supports manual processes initially, automated over time
4. **Developer Platform Providers**: Pluggable components that integrate with downstream systems. Key insight: enables inner-sourcing (other teams contribute providers without maintaining core platform code)
5. **User Profile and Team Metadata**: RBAC, discovery, and data aggregation; multi-role teams (not just identity provider groups)

**Automation design principle**: "Design for automation from the start." Even when implementing manual processes initially (via Power Automate flows), design them so they can be replaced by full automation later. Start with what you have, prove value, expand.

**Provider model for inner-sourcing**: The pluggable provider interface allows independently-written code to plug into core functionality. Other teams can contribute providers without needing to maintain core platform code. Solves the classic inner-sourcing problem where teams contribute but can't maintain.

**Users vs. Teams**: Identity provider groups are for managing membership; teams (multi-role, multi-group) are the right abstraction for RBAC and data aggregation in a platform context. Teams-as-Code (TaC) pattern: a secure Git repo is the source of a team's definition.

---

## Connections

- [[concepts/internal-developer-platform]] — Microsoft's architectural components complement Humanitec's IDP definition
- [[concepts/developer-self-service]] — the automation-first principle extends existing self-service concepts
- [[topics/platform-engineering]] — comprehensive technical architecture reference from a major cloud provider
