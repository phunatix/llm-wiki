---
title: Kubernetes Logging in Production
type: source
status: active
created: 2026-04-10
updated: 2026-04-10
source_files:
  - raw/sources/Kubernetes Logging in Production.md
tags:
  - source
  - kubernetes
  - logging
  - observability
---

# Summary

This source explains cluster-level logging in Kubernetes and compares the DaemonSet and sidecar patterns for collecting logs from applications and system components. It focuses on practical tradeoffs in flexibility, complexity, resource consumption, and debuggability.

# Key Takeaways

- Node-level DaemonSet collection is simpler and more resource-efficient for common cases.
- Sidecars are more flexible for nonstandard logging patterns but add complexity and overhead.
- Logging architecture should be chosen with awareness of storage, access, and operational tradeoffs.

# Relationships

- Supports [Kubernetes](../concepts/kubernetes.md).
- Related to [Site Reliability Engineering](../concepts/site-reliability-engineering.md).

# Open Questions

- Should the wiki capture a broader observability concept that ties together logging, metrics, and tracing?
