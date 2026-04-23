---
title: Governance by Default
type: concept
source_count: 1
created: 2026-04-10
last_updated: 2026-04-23
tags: [governance, platform-engineering, policy-as-code, compliance, security]
inbound_links: 0
status: complete
related_pages: ["[[concepts/golden-paths]]", "[[concepts/agentic-infrastructure]]", "[[concepts/model-context-protocol]]", "[[concepts/internal-developer-platform]]", "[[topics/platform-engineering]]"]
---

# Governance by Default

**Domain**: Platform Engineering / Security & Compliance

**One-line definition**: The platform design pattern of encoding policy, security, and compliance controls into the delivery path itself — so that valid, compliant behavior is the easiest path, and invalid deployments are difficult or impossible to produce without deliberate override.

---

## The Core Principle

Traditional governance is **post-hoc**: a policy team reviews what was deployed and flags violations. This creates audit fatigue, lag between violation and detection, and adversarial dynamics between developers and compliance.

Governance by default inverts this:
- Security baselines are embedded in deployment templates
- Policy-as-code runs at build/deploy time, not audit time
- Non-compliant configurations are rejected by the platform, not caught by a human reviewer
- Compliant behavior requires no extra effort from the developer — it's simply what the platform produces

The goal is to make the secure path identical to the easy path.

---

## Mechanisms

| Mechanism | How It Works |
|---|---|
| **Policy-as-code** | Security/compliance rules expressed as code (OPA, Kyverno, Sentinel) that run in CI/CD or admission controllers |
| **Service templates** | Pre-approved scaffolding that includes security defaults (network policies, RBAC, secrets management) |
| **Admission controllers** | Kubernetes-layer enforcement; rejects resources that violate policy before they reach the cluster |
| **Automatic control injection** | Sidecar injection, log forwarding, certificate issuance happen automatically — not by developer choice |
| **Guardrails over gates** | Defines boundary conditions (outcomes), not implementation methods — see [[concepts/golden-paths]] |

---

## Relationship to Golden Paths

Governance by default and [[concepts/golden-paths]] are complementary:

- **Golden paths** define *how* to do things in the recommended way — optimizing for developer experience and speed
- **Governance by default** ensures the golden path is also the *compliant* way — optimizing for security and auditability

When well-implemented, developers get both: the fast path and the safe path are the same path.

A golden cage is what happens when governance is enforced without golden paths — compliance requirements with no supported route through them. Governance by default requires both: the control *and* the supported way to work within it.

---

## Why This Matters More With AI

The volume and variability of changes moving through delivery pipelines increases significantly when AI agents generate code and trigger deployments autonomously. Manual review cannot scale to match:

- AI agents may generate configurations that technically work but violate security baselines
- The speed advantage of agentic coding disappears if every output requires human compliance review
- Governance by default is the only viable path: controls embedded in the platform catch violations automatically, before they reach production

This connects directly to [[concepts/agentic-infrastructure]]: platforms that treat AI agents as first-class actors need to govern agent actions the same way they govern human developer actions — through embedded controls, not post-hoc audits.

---

## Key Ideas

- Platform teams reduce compliance burden by embedding controls directly into delivery defaults
- Policy-as-code, service templates, and automatic control injection are the primary mechanisms
- Governance by default scales with agent-driven development in a way that manual review cannot
- The boundary between enabling governance and over-constraining teams is a real design question — too many controls break developer experience

---

## Open Questions

- Where is the boundary between platform-level governance and service-team-level ownership?
- Which controls belong in platform defaults versus downstream policies teams manage themselves?
- As AI-generated code becomes common, how do we verify that the generated output passes governance controls without human review of every line?

---

## Sources

- [[sources/10-platform-engineering-predictions-2026]] — "10 Platform Engineering Predictions for 2026"; governance by default as predicted platform evolution; policy-as-code; AI-generated code driving adoption
