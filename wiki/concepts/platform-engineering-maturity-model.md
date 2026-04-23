---
title: Platform Engineering Maturity Model
type: concept
source_count: 1
created: 2026-04-10
last_updated: 2026-04-23
tags: [platform-engineering, maturity-model, cncf, organizational-design]
inbound_links: 0
status: complete
related_pages: ["[[topics/platform-engineering]]", "[[concepts/internal-developer-platform]]", "[[concepts/cognitive-load]]", "[[entities/Humanitec]]", "[[entities/cncf]]"]
---

# Platform Engineering Maturity Model

**Domain**: Platform Engineering / Organizational Capability

**One-line definition**: A CNCF-backed framework for assessing how an organization's platform discipline is evolving across five independent dimensions — intended to surface the next improvements worth pursuing, not to assign a simplistic overall grade.

---

## The Model

The maturity model evaluates platform engineering across five aspects independently:

| Aspect | What It Measures |
|---|---|
| **Investment** | Budget, headcount, leadership commitment to the platform function |
| **Adoption** | How many teams and workflows are using the platform; voluntary vs. mandated |
| **Interfaces** | Quality of the developer-facing surface: APIs, CLIs, portals, documentation |
| **Operations** | Reliability, incident response, SLOs, on-call for the platform itself |
| **Measurement** | Metrics, feedback loops, DORA/SPACE tracking, platform ROI |

Each aspect progresses through four stages:
1. **Provisional** — ad hoc, informal, reactive
2. **Operational** — consistent, documented, managed
3. **Scalable** — self-service, automated, team-independent
4. **Optimizing** — continuously improving, data-driven, proactively evolving

---

## How to Use It

The model is a diagnostic, not a race to "Stage 4." Key principles:

- **Assess each dimension independently.** An organization can be Scalable on Interfaces and Provisional on Measurement simultaneously; that's normal and useful to know.
- **Context determines target.** A 10-person startup may never need to optimize Investment tracking. A 5,000-person platform team probably should.
- **Advancing costs resources.** Higher maturity requires more coordination, tooling, and process. Advancement should be justified by outcomes, not by a desire to score well.
- **Use it to find the next bottleneck.** The goal is identifying the weakest dimension that, if improved, would most unlock platform value — a Theory of Constraints lens applied to platform capability.

---

## Relationship to Broader Frameworks

The CNCF model connects to:

- The **Platforms White Paper** (CNCF) — defines what a good platform provides
- The **Cloud Native Maturity Model** — assesses cloud-native adoption more broadly
- **DORA metrics** — DevOps Research and Assessment data on deployment frequency, lead time, change failure rate, MTTR
- **SPACE framework** — Satisfaction, Performance, Activity, Communication/Collaboration, Efficiency — a richer developer productivity model

The platform engineering maturity model can be used alongside DORA/SPACE metrics to correlate platform investment with engineering outcomes.

---

## Common Failure Patterns

- **Measuring adoption as success** — high adoption of a bad platform is not an achievement; use DORA/SPACE to check if the platform is improving outcomes, not just uptake
- **Advancing uniformly** — trying to move all five dimensions in lockstep diffuses effort; go deep on one bottleneck at a time
- **Ignoring culture** — the Humanitec/DORA survey ("What's the Future of Platform Engineering?") finds that platform engineering is 90% cultural; the maturity model captures the technical/process layer but not organizational dynamics

---

## Open Questions

- Should the model include a dimension for **AI governance** (as AI agents become platform actors)?
- How does this model compare to other maturity frameworks in adjacent domains (security maturity, data platform maturity)?
- The current source includes the top-level model but not per-aspect descriptors in detail — a more complete source may warrant revisiting this page.

---

## Related Pages

- [[topics/platform-engineering]] — broader context and key debates in the discipline
- [[concepts/internal-developer-platform]] — the technical artifact being assessed
- [[concepts/cognitive-load]] — the key outcome metric the model indirectly serves
- [[entities/cncf]] — publishes and stewards the model
- [[entities/Humanitec]] — major contributor to platform engineering research and tooling

---

## Sources

- [[sources/platform-engineering-maturity-model]] — Primary source; CNCF working group; five aspects; four stages; connection to Platforms White Paper and Cloud Native Maturity Model
