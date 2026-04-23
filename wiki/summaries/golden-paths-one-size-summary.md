---
title: "Summary: Golden Paths — One Size Does Not Fit All"
type: summary
source_count: 1
created: 2026-04-23
last_updated: 2026-04-23
tags:
  - summary
  - golden-path
  - platform-engineering
  - developer-experience
source_file: "raw/inbox/Golden Paths One Size Does Not Fit All.md"
related_pages:
  - concepts/golden-paths
  - topics/platform-engineering
  - concepts/developer-self-service
status: complete
---

# Summary: Golden Paths — One Size Does Not Fit All

**Source**: chieftherapyofficer.co.uk — "Golden Paths: One Size Does Not Fit All"
**Author**: Bryan Ross
**URL**: https://www.chieftherapyofficer.co.uk/p/golden-paths-one-size-does-not-fit
**Published**: 2025-11-22 | **Clipped**: 2026-04-23
**Type**: Opinion / practitioner framework; newsletter post

---

## What This Source Contains

A practitioner framework for resolving the fundamental tension between platform standardization and developer autonomy. Introduces "guardrails over gates" as the organizing principle, with a four-part framework for building platforms that developers choose to use. Includes a real case study where this approach raised adoption from 17% to 86% in six months.

---

## Key Takeaways

### The Fundamental Conflict
Platform teams optimize for standardization and reliability (global rationality). Developers optimize for solving their specific problem as fast as possible (local rationality). **Individual teams making locally rational decisions create organizational fragmentation.** The usual response — mandating full adoption, closing escape hatches — pushes workarounds underground, reducing visibility rather than compliance.

### Guardrails over Gates
Guardrails define boundary conditions, not implementation. They answer: what organizational risk does requiring a specific implementation prevent? Where the risk is low, flexibility wins.

**Case study**: Financial services firm. Three non-negotiable guardrails:
1. All production deployments pass security baseline
2. All services emit standardized metrics to the observability platform
3. All secrets retrieved from secrets management at runtime

Everything else: flexible. Result: 17% → 86% adoption in six months. Platform team relationship with developers shifted from adversarial to collaborative.

### Components over Completeness
Stop thinking of "the platform" as a thing teams use or don't. Build composable capabilities that teams can adopt incrementally. Security scanning as a service (not a mandatory tool — just standardized SARIF output format). Deployment automation as a service. Secrets retrieval as a service.

Teams compose from components. More adoption = less undifferentiated heavy lifting. The platform becomes more attractive the more you use it — without being mandatory at any level.

### Exception Handling by Design
Edge cases are real. Build overrides into the platform itself:
- An `override_security_scan` flag with a required justification
- Deployment proceeds + notification to security team + weekly review log
- Pattern analysis from overrides reveals where guardrails need adjustment

This maintains visibility while giving developers legitimate escape hatches, preventing them from abandoning the platform entirely.

### The Key Reframe
> "I've watched this transformation happen at organisations ranging from 20 to 20,000 engineers. The mechanics vary, but the fundamental shift remains the same: from standardisation through control, to standardisation through attraction."

The measure of a platform isn't adoption rate — it's whether developers would choose it even if they weren't required to.

---

## Connections to Existing Wiki

- **[[concepts/golden-paths]]** — guardrails/gates framing and 17%→86% case study are core contributions to the concept page
- **[[concepts/developer-self-service]]** — the composable building blocks approach is the right model for self-service design
- **[[topics/platform-engineering]]** — the standardization-through-attraction principle addresses the central cultural challenge in platform engineering
