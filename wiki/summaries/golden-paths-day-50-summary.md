---
title: "Summary: How to Pave Golden Paths That Actually Go Somewhere"
type: summary
source_count: 1
created: 2026-04-23
last_updated: 2026-04-23
tags:
  - summary
  - golden-path
  - platform-engineering
  - dynamic-configuration
  - humanitec
source_file: "raw/inbox/How to pave golden paths that actually go somewhere.md"
related_pages:
  - concepts/golden-paths
  - concepts/internal-developer-platform
  - entities/Humanitec
  - entities/Kaspar-von-Grunberg
  - topics/platform-engineering
status: complete
---

# Summary: How to Pave Golden Paths That Actually Go Somewhere

**Source**: platformengineering.org — "How to pave golden paths that actually go somewhere"
**Author**: Aeris Ransom (platformengineering.org)
**URL**: https://platformengineering.org/blog/how-to-pave-golden-paths-that-actually-go-somewhere
**Published**: 2023-12-13 | **Clipped**: 2026-04-23
**Type**: Analysis / methodology article; Kaspar von Grünberg's PlatformCon 2023 talk

---

## What This Source Contains

A synthesis of Kaspar von Grünberg's (Humanitec CEO) research on where platform teams go wrong with golden paths, why Day 2–50 is more valuable than Day 1, a prioritization framework for path selection, and Dynamic Configuration Management as the technical solution to the root cause of most ongoing friction.

---

## Key Takeaways

### The Core Mistake: Day 1 Optimization
Most platform teams prioritize golden paths for service creation (scaffolding, provisioning). The error: **service creation is below 1% of the total time invested in an application** across its lifecycle. Optimizing Day 1 produces minimal ROI.

> "Of the time your team will invest in an application, the creation process is below 1%."

The right target is **Day 2–50**: the ongoing operations that consume the other 99%. Deployments, configuration changes, rollbacks, debugging, waiting for other teams, resource updates.

### The Prioritization Framework
von Grünberg's exercise: score potential golden paths by `frequency × (dev time + ops time including wait)`. High frequency + high wait time = highest ROI.

Most common high-value pain points across thousands of engineering orgs:
- **Waiting for other teams** (6.3% of deployments, 32+ hours of combined time)
- **Debugging / error tracing** (4.4%, 20 hours)
- **Configuration changes** (5%, but lower time)
- **Rollbacks** (1.75%, 30 hours combined)

### The Root Cause: Static Configuration Management
Most IDPs fail ongoing operations because they use static configuration files manually scripted against static environments. When infrastructure changes (adding a database, updating a dependency), developers either manage it manually (shadow ops) or submit a ticket (ops bottleneck). Neither scales.

### The Solution: Dynamic Configuration Management (DCM)
DCM (Humanitec's methodology): developers write workload specifications describing what they need; the platform orchestrator dynamically generates environment-specific configurations.

**RMCD pattern**: Read spec → Match resource templates → Create configs → Deploy wired to dependencies.

Practical outcome:
- Updating Postgres version: update one resource definition, auto-propagate across all workloads
- Adding a new database type: one resource definition addition, reusable by all teams
- No manual environment-specific config maintenance

DCM turns every day into a potential Day 1: a fresh starting point for optimization rather than accumulated technical debt.

---

## Connections to Existing Wiki

- **[[concepts/golden-paths]]** — Day 1 vs Day 2–50 prioritization and DCM are now integrated into the concept page
- **[[entities/Humanitec]]** — von Grünberg's frameworks; Platform Orchestrator and Score are the DCM implementation
- **[[concepts/cognitive-load]]** — DCM directly reduces ongoing cognitive load by eliminating manual config management
