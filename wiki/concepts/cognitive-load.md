---
title: Cognitive Load
type: concept
source_count: 2
created: 2026-04-13
last_updated: 2026-04-13
tags: [platform-engineering, developer-experience, devops]
inbound_links: 0
status: complete
related_pages: ["[[concepts/developer-self-service]]", "[[concepts/golden-paths]]", "[[concepts/internal-developer-platform]]", "[[entities/Humanitec]]"]
---

# Cognitive Load

**Domain**: Platform Engineering / Developer Experience

**One-line definition**: The mental effort required of developers to understand and operate the systems they work with — the key metric for evaluating platform and self-service design.

## Definition

Cognitive load in the software context refers to how much mental bandwidth developers must spend on infrastructure, tooling, and operational concerns rather than on solving their core domain problem. High cognitive load from operational complexity directly reduces development quality and speed.

The concept was popularized in platform engineering by [[entities/Kaspar-von-Grunberg]] of [[entities/Humanitec]] as the central lens for evaluating developer self-service designs.

## The Cognitive Load Spectrum

```
Low complexity                                    High complexity
Low cognitive load ←───────────────────────────→ High cognitive load

[Heroku: one tool]          [Balanced IDP]          [EKS + Terraform + Argo +
                                                      Helm + Jenkins + Snyk...]
     ↑                           ↑                           ↑
Golden cage risk          Optimal zone               Overwhelm risk
(over-abstraction)        (golden paths)             (thrown over fence)
```

## The Two Failure Modes

1. **"Throw everything at them"**: Operations teams dump complex toolchains onto developers under the banner of "you build it, you run it." Developers don't actually know how to operate it, productivity drops, ops still gets paged.

2. **"Take it all from them" (Golden cage)**: Platform team builds an opaque black box. Developers don't understand what's happening, can't handle edge cases, lose trust, eventually revolt and abandon the platform.

## How to Find the Right Balance

- **Communication**: Ask developers what they want to operate; don't assume
- **Observe willingness to handle complexity**: Some teams want more control, others less
- **Team-by-team calibration**: Cognitive load tolerance varies

## Key Insight

> "97% of developers stick to a golden path once established, following the 'social contract' that staying on the path makes the setup more scalable." — Kaspar von Grünberg, Humanitec

The right level of abstraction enables developers to understand what's under the hood (building trust) while reducing the operational burden to a manageable level.

## See Also

- [[concepts/golden-paths]]: The design pattern that manages cognitive load correctly
- [[concepts/developer-self-service]]: The broader principle
- [[concepts/internal-developer-platform]]: The tool category
- [[topics/platform-engineering]]

## Sources

- [[summaries/dark-side-of-self-service--summary]]: Primary source for the cognitive load model
- [[summaries/whats-the-future-of-platform-engineering--summary]]: "10% technical, 90% cultural" framing
