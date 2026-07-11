---
title: Backstage
type: entity
source_count: 2
created: 2026-07-09
last_updated: 2026-07-09
tags:
  - entity
  - platform-engineering
  - developer-portal
  - open-source
related_pages:
  - concepts/internal-developer-platform
  - concepts/golden-paths
  - topics/platform-engineering
  - entities/Humanitec
status: complete
---

# Backstage

**Type**: Open-source developer portal framework
**Created by**: Spotify (internal use since ~2016; open-sourced 2020)
**License**: Apache 2.0
**Repository**: https://github.com/backstage/backstage
**Steward**: CNCF (Cloud Native Computing Foundation) — joined 2022

## What It Is

Backstage is an open-source developer portal framework that serves as the foundation for Internal Developer Platforms. It provides the scaffolding — software catalog, plugin system, TechDocs, templating — on which platform teams build their organization-specific developer experience.

The core insight: instead of every company building a developer portal from scratch, Backstage provides a composable base. Organizations extend it with plugins (first-party, community, and internal) to cover their specific tooling ecosystem.

## Core Components

- **Software Catalog**: The heart of Backstage — a unified registry of all components, APIs, teams, users, systems, and domains. Entities are defined in YAML and synced from source of truth systems.
- **Scaffolder**: Golden path templates for creating new services, repositories, and infrastructure. Developers self-serve without waiting for ops.
- **TechDocs**: Docs-as-code — Markdown documentation automatically rendered and surfaced in the portal.
- **Plugin system**: The extensibility model. Hundreds of community plugins; organizations build internal plugins for proprietary tooling.
- **Search**: Cross-catalog search across all entities and docs.

## Adoption at Scale: Zalando's Sunrise

Zalando deployed a Backstage-based portal called **Sunrise** starting 2021, managed by a team of 4 engineers:
- Replaced 100+ disconnected interfaces and the previous developer console
- 40,000+ registered entities (applications, teams, users) synced daily from source-of-truth systems
- 30 front-end plugins covering 27 integrated tools/services across the full SDLC
- Inner-sourcing model: 10+ plugins owned by teams outside the platform team; standard component library reduces contributor friction
- Personalization for users who don't own components themselves — increased adoption among principal engineers and leadership

**Key Zalando adoption lessons**:
1. **Kill old tooling**: "The most impactful thing was redirecting users from old features and *completely shutting down* the old tooling." Habit and bookmarks win over better alternatives unless the old option disappears.
2. **Personalization drives adoption**: Users who don't own services directly still engage when content is personalized to their accountability
3. **UX research is critical**: Cohesive experience as Backstage grows requires investment in design — not just feature shipping
4. **Open-source upstream selectively**: Zalando contributes back when issues affect all Backstage adopters; keeps company-specific logic internal

## Relationship to Golden Paths

Backstage was built by Spotify specifically to surface and deliver golden paths. The Backstage "Explore" section visualizes "blessed tools" per engineering discipline. The Software Catalog and Scaffolder implement the golden path philosophy: discoverable defaults, step-by-step tutorials, self-service execution.

## See Also

- [[concepts/internal-developer-platform]] — Backstage is the most widely-adopted IDP portal layer
- [[concepts/golden-paths]] — Backstage was Spotify's implementation vehicle for golden paths
- [[entities/Humanitec]] — Platform orchestrator that complements Backstage (Backstage = catalog/portal; Humanitec = deployment orchestration)

## Sources

- [[summaries/zalando-sunrise-backstage-summary]] — Zalando's Sunrise: adoption lessons, entity scale, inner-sourcing model, shutdown-old-tooling insight
- [[summaries/spotify-golden-paths-summary]] — Backstage as the interface where golden paths are surfaced and consumed at Spotify
