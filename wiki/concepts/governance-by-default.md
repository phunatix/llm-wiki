---
title: Governance By Default
type: concept
status: active
created: 2026-04-10
updated: 2026-04-10
source_files:
  - raw/sources/10 Platform engineering predictions for 2026.md
tags:
  - concept
  - governance
  - compliance
  - platform-engineering
---

# Summary

Governance by default is the platform pattern of making compliant and secure behavior the built-in path rather than an optional afterthought. Instead of relying on manual review or post-hoc detection, the platform encodes policy into templates, controls, and infrastructure constraints so invalid deployments are difficult or impossible to produce.

# Key Ideas

- Platform teams can reduce compliance burden by embedding controls directly into delivery defaults.
- Policy-as-code, service templates, and automatic control injection are examples of governance mechanisms becoming part of the platform surface itself.
- This pattern becomes more important as AI-generated code and autonomous agents increase the volume and variability of changes moving through the system.

# Related Concepts

- [Platform Engineering](platform-engineering.md)
- [Agentic Infrastructure](agentic-infrastructure.md)

# Evidence

- Derived from [10 Platform engineering predictions for 2026](../sources/10-platform-engineering-predictions-2026.md).

# Open Questions

- Where is the boundary between enabling governance and over-constraining teams?
- Which controls belong in platform defaults versus in downstream service ownership?
