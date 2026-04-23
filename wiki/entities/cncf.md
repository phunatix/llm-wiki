---
title: CNCF
type: entity
source_count: 1
created: 2026-04-10
last_updated: 2026-04-23
tags: [organization, cncf, cloud-native, open-source, platform-engineering]
inbound_links: 0
status: complete
related_pages: ["[[concepts/platform-engineering-maturity-model]]", "[[concepts/kubernetes]]", "[[topics/platform-engineering]]"]
---

# CNCF (Cloud Native Computing Foundation)

**Type**: Non-profit standards body / Open-source foundation

**Parent**: Linux Foundation

**One-line description**: The foundation that stewards Kubernetes, the Platform Engineering Maturity Model, and the broader cloud-native ecosystem — the organizational home for defining what "cloud-native" means and how organizations should evolve their platform capabilities.

---

## Role in This Wiki

CNCF appears primarily as:
1. **Publisher of the Platform Engineering Maturity Model** — a CNCF working group produced the maturity model used to assess platform discipline across five dimensions (see [[concepts/platform-engineering-maturity-model]])
2. **Steward of Kubernetes** — CNCF took over Kubernetes governance from Google in 2016; Kubernetes is the infrastructure substrate for much of what this wiki covers (see [[concepts/kubernetes]])
3. **Framing institution** — CNCF's Platforms White Paper and Cloud Native Maturity Model provide definitional context for what "platform engineering" means at an industry level

---

## Key Published Standards and Frameworks

| Document | Purpose |
|---|---|
| **Platform Engineering Maturity Model** | Assess organizational platform capability across five aspects |
| **Platforms White Paper** | Defines what good internal platforms provide |
| **Cloud Native Maturity Model** | Assesses overall cloud-native adoption |
| **CNCF Landscape** | Catalog of cloud-native projects and tools |

---

## Governance Model

CNCF operates as a vendor-neutral home for cloud-native projects. Projects go through three stages:
- **Sandbox** — early-stage exploration
- **Incubating** — growing adoption and governance
- **Graduated** — production-proven, with defined governance

Kubernetes, Prometheus, Envoy, and many others are graduated projects.

---

## Significance for Platform Teams

When CNCF publishes a framework (like the Platform Engineering Maturity Model), it carries weight because:
- Multiple vendors contributed and agreed on it
- It reflects practitioner consensus across diverse organizations
- It tends to become the reference point in enterprise conversations about platform strategy

This means CNCF framing shapes how platform engineering is defined, measured, and sold internally — it's worth understanding where CNCF definitions diverge from vendor claims.

---

## Open Questions

- If more CNCF documents are ingested (Cloud Native Maturity Model, Platforms White Paper, TAG App Delivery outputs), this page should expand to capture specific working groups and their outputs
- How does CNCF's definition of platform engineering align with (or diverge from) Humanitec's IDP framing?

---

## Sources

- [[sources/platform-engineering-maturity-model]] — Primary CNCF working-group document; references Platforms White Paper and Cloud Native Maturity Model; CNCF as publisher and framing institution
