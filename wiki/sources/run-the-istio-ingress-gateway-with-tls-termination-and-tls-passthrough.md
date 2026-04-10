---
title: Run the Istio ingress gateway with TLS termination and TLS passthrough
type: source
status: active
created: 2026-04-10
updated: 2026-04-10
source_files:
  - raw/sources/Run the Istio ingress gateway with TLS termination and TLS passthrough – Daniel's Tech Blog.md
tags:
  - source
  - kubernetes
  - istio
  - ingress
---

# Summary

This source is a configuration-oriented note showing that the default Istio ingress gateway can support both TLS termination and TLS passthrough at the same time. The captured local copy is somewhat messy, but the core point is about combining both modes in one gateway setup.

# Key Takeaways

- Istio supports both TLS termination and TLS passthrough.
- The source’s central question is whether both can coexist on the same ingress gateway, and its answer is yes.
- The value of the article is mainly operational configuration detail rather than conceptual argument.

# Relationships

- Supports [Kubernetes](../concepts/kubernetes.md).

# Open Questions

- The local clipping appears incomplete or poorly formatted; a cleaner copy may be worth ingesting later if ingress topics become central.
