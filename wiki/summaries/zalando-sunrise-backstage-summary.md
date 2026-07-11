---
title: "Summary: Sunrise — Zalando's Developer Platform Based on Backstage"
type: summary
source_count: 1
created: 2026-07-09
last_updated: 2026-07-09
tags:
  - summary
  - platform-engineering
  - internal-developer-platform
  - backstage
  - developer-experience
source_file: "raw/inbox/Sunrise Zalando's developer platform based on Backstage.md"
related_pages:
  - entities/Backstage
  - concepts/internal-developer-platform
  - concepts/golden-paths
  - topics/platform-engineering
status: complete
---

# Summary: Sunrise — Zalando's Developer Platform Based on Backstage

**Source**: Zalando Engineering Blog — "Sunrise: Zalando's developer platform based on Backstage"
**Author**: Lacey Nagel (Product) & Arthur (Engineering Lead)
**URL**: https://engineering.zalando.com/posts/2023/08/sunrise-zalandos-developer-platform-based-on-backstage.html
**Published**: 2023-08-03 | **Clipped**: 2026-07-07
**Type**: Case study / practitioner interview

---

## What This Source Contains

An interview-format case study of Zalando's adoption of Backstage to build "Sunrise," their internal developer portal. Covers the before-state (100+ disconnected interfaces), the build decision (limited resources → open-source foundation), adoption tactics, scale challenges, inner-sourcing model, upstream contribution approach, and future vision.

---

## Key Takeaways

### The Before State
Before Sunrise: 100+ disconnected interfaces. A prior "Developer Console" centralized links but only covered Code-through-Deploy steps. Engineers maintained long bookmark lists and habit-built workarounds. The problem wasn't tools — it was fragmentation.

### Why Backstage
- Limited resources at the time (few engineers, limited design capacity)
- Backstage provided out-of-the-box design system + Software Catalog plugin
- Spotify reached out while Zalando was still in discovery phase
- Key: need to deliver fast enough to justify strategic investment

### Scale
- 40,000+ registered entities (applications, teams, users) synced daily
- 30 front-end plugins covering 27 integrated tools/services
- 2,000+ PRs merged to Sunrise repository
- Team: 4 engineers (Builder Portal team)
- 10+ plugins owned by teams outside the core platform team

### The #1 Adoption Lever: Kill Old Tooling
> "What turned out to be most impactful for solving this problem is ensuring that we redirect users from old features to the new ones in Sunrise shortly after making them generally available and then *completely shut down* the old tooling."

People cling to bookmarks and habits. A better alternative doesn't win if the old alternative still exists. This is the operational lesson most platform teams avoid because it requires cross-team negotiation and accepting disruption.

### Other Adoption Drivers
- **Personalization**: Personalized homepage (open PRs, recently deployed pipelines, Cyber Week dashboard) drives return visits from users who don't own services — principal engineers, leadership
- **Interoperability**: Not just "find things" — seamlessly completing tasks *between* tools reduces the cognitive overhead of context-switching

### Inner-Sourcing Model
Other teams own and maintain their own plugins. Barrier: Backstage's domain-specific language + Zalando's standards are unfamiliar to platform-unfamiliar engineers. Solution: invest in standard component library + documentation so contributors spend time on UX, not boilerplate. This is the scalability mechanism for a 4-engineer team covering a large engineering org.

### Open-Source Contribution Approach
Zalando upstream-contributes when problems affect all Backstage adopters. Proprietary/Zalando-specific logic stays internal. Plugin open-sourcing is selective (API Linter plugin released; others kept internal). Recommendation: engage with the community, don't shy away from relying on well-maintained community plugins.

### Future Vision
Comprehensive entity graph: mapping relationships between applications, data pipelines, teams, and business domains — automatically where possible. Goal: shift-left not just security/compliance but also productivity, reliability, and cost efficiency by surfacing operational health in relationship to business metrics.

---

## Connections to Existing Wiki

- **[[entities/Backstage]]** — Zalando's experience is the primary real-world scale data point for Backstage adoption
- **[[concepts/internal-developer-platform]]** — The 100+ interfaces → unified portal transformation is a canonical IDP success story; the shutdown-old-tooling lesson is the adoption insight missing from most IDP guidance
- **[[concepts/golden-paths]]** — Personalized homepage + CI/CD integration are golden paths for Zalando's Day 2–50 operations (not scaffolding)
- **[[concepts/developer-self-service]]** — Inner-sourcing model: 4-engineer team enabling org-wide contribution via standard components
