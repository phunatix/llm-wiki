---
title: Golden Paths
type: concept
source_count: 2
created: 2026-04-13
last_updated: 2026-04-13
tags: [platform-engineering, developer-experience, devops]
inbound_links: 0
status: complete
related_pages: ["[[concepts/cognitive-load]]", "[[concepts/developer-self-service]]", "[[concepts/internal-developer-platform]]", "[[entities/Humanitec]]"]
---

# Golden Paths

**Domain**: Platform Engineering / Developer Experience

**One-line definition**: Opinionated, well-maintained default paths through a developer platform that abstract complexity without restricting developer freedom — the correct alternative to "golden cages."

## Definition

A golden path is a curated route through the tooling and infrastructure of an organization that handles common use cases elegantly. Developers who stay on the golden path benefit from a smooth experience with reduced cognitive load. Crucially, the path is transparent (developers understand what's under the hood) and escapable (developers can go off-path when needed — they're just not forced to).

**Contrast with golden cage**: A golden cage is an abstraction that's opaque and inescapable. Developers don't understand what's happening, can't handle edge cases, and lose trust in the system.

## Key Properties of a Good Golden Path

1. **Transparent**: Developers understand what the path does, even if they don't operate it
2. **Escapable**: Developers can go low-level when they need to — the path is a shortcut, not a wall
3. **97% coverage**: Paths work for the vast majority of cases; edge cases can be handled manually
4. **Socially contracted**: Developers choose the path because they see value, not because they're forced
5. **Iterative**: Built with developer feedback; paths evolve with team needs

## Why This Matters

> "If your abstractions work in 90% of cases but the remaining 10% are a pain, you don't win much." — Kaspar von Grünberg

Golden paths that cover 97%+ of use cases are effective. Developers trust them, follow them, and benefit from the reduced cognitive load. The 3% who go off-path can do so without breaking down.

## Examples

- Spotify: 99% internal platform adoption rate (voluntary) — achieved through golden paths, not mandates
- GitHub: Internal developer platform with golden paths; developers stay on path while retaining ability to go low-level
- Any good CI/CD pipeline template is a golden path

## Relationship to Internal Developer Platforms

[[concepts/internal-developer-platform]]s are the technical implementation of golden paths. A good IDP makes the golden path the path of least resistance — not the only path.

## See Also

- [[concepts/cognitive-load]]
- [[concepts/developer-self-service]]
- [[concepts/internal-developer-platform]]
- [[topics/platform-engineering]]

## Sources

- [[summaries/dark-side-of-self-service--summary]]: Primary source; contrasts golden paths vs. golden cages
- [[summaries/whats-the-future-of-platform-engineering--summary]]: Cultural dimension of golden path adoption
