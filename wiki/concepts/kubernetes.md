---
title: Kubernetes
type: concept
status: active
created: 2026-04-10
updated: 2026-04-10
source_files:
  - raw/sources/An Introduction to Kustomize - Scott's Weblog - The weblog of an IT pro focusing on cloud computing, Kubernetes, Linux, containers, and networking.md
  - raw/sources/Building Multi-Tenant Kubernetes on Azure AKS.md
  - raw/sources/Kubernetes Logging in Production.md
  - raw/sources/Nomad, Kubernetes, and a Pragmatic Look at Choosing Orchestrators.md
  - raw/sources/Run Kubernetes in Azure the Cheap Way.md
  - raw/sources/Run the Istio ingress gateway with TLS termination and TLS passthrough – Daniel's Tech Blog.md
  - raw/sources/Talos Ein Minimal-Linux für Kubernetes.md
  - raw/sources/The rise and future of Kubernetes and open source at Google  Google Cloud Blog.md
tags:
  - concept
  - kubernetes
---

# Summary

Kubernetes is the central infrastructure substrate across much of this wiki. In the current source set it appears as both a practical orchestration platform that requires decisions about networking, logging, ingress, tenancy, and operating systems, and as a larger cloud-native ecosystem shaped by open source governance and managed-service tradeoffs.

# Key Ideas

- Kubernetes is powerful precisely because it creates a common control plane for application deployment and operations, but that power introduces real operational complexity.
- Practical Kubernetes design depends on surrounding choices such as ingress patterns, manifest customization, tenancy boundaries, logging architecture, and host operating systems.
- Managed Kubernetes and adjacent tooling often shift effort from raw mechanics toward policy, reliability, and developer enablement.

# Related Concepts

- [Platform Engineering](platform-engineering.md)
- [Site Reliability Engineering](site-reliability-engineering.md)
- [Internal Developer Platforms](internal-developer-platforms.md)

# Evidence

- Manifest customization is covered in [An Introduction to Kustomize](../sources/introduction-to-kustomize.md).
- Shared-cluster design appears in [Building Multi-Tenant Kubernetes on Azure AKS](../sources/building-multi-tenant-kubernetes-on-azure-aks.md).
- Operational logging patterns appear in [Kubernetes Logging in Production](../sources/kubernetes-logging-in-production.md).
- Broader strategic framing appears in [The rise and future of Kubernetes and open source at Google](../sources/the-rise-and-future-of-kubernetes-and-open-source-at-google.md).

# Open Questions

- Which Kubernetes topics deserve deeper first-class pages next: ingress, tenancy, observability, or cluster operating systems?
- How much of the repo should remain Kubernetes-specific versus using Kubernetes as one example of platform design?
