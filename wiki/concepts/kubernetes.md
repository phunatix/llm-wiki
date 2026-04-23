---
title: Kubernetes
type: concept
source_count: 8
created: 2026-04-10
last_updated: 2026-04-23
tags: [kubernetes, devops, platform-engineering, container-orchestration, cloud-native]
inbound_links: 0
status: complete
related_pages: ["[[concepts/internal-developer-platform]]", "[[concepts/sre-anything-framework]]", "[[concepts/platform-engineering-maturity-model]]", "[[topics/devops-homelab]]", "[[topics/platform-engineering]]"]
---

# Kubernetes

**Domain**: Container Orchestration / Cloud-Native Infrastructure

**One-line definition**: The dominant open-source container orchestration platform; in this wiki, both a practical infrastructure substrate requiring significant design decisions and a larger cloud-native ecosystem shaped by open-source governance and managed-service tradeoffs.

---

## What Kubernetes Is

Kubernetes (K8s) provides a control plane for deploying, scaling, and operating containerized workloads. It abstracts away the underlying compute layer, but introduces its own operational complexity — networking models, storage drivers, ingress patterns, multi-tenancy boundaries, observability pipelines, and host OS choices all require deliberate decisions.

The platform is powerful precisely because it creates a common API surface for application delivery. That same API surface is also why "just use Kubernetes" understates what teams actually take on.

---

## Practical Design Decisions

### Manifest Customization
Kubernetes deployments are config-heavy. **Kustomize** is one approach to managing per-environment overlays without templating; it layers patches on a base manifest set. This keeps YAML manageable across dev/staging/prod without duplicating configuration. (See [[sources/introduction-to-kustomize]])

### Multi-Tenancy
Shared clusters require explicit tenancy design — namespace isolation, RBAC, network policies, resource quotas. Multi-tenant Kubernetes on managed services (e.g., AKS) introduces additional tradeoffs between isolation strength and operational overhead. (See [[sources/building-multi-tenant-kubernetes-on-azure-aks]])

### Logging Architecture
Production logging at the Kubernetes layer involves sidecar vs. node-agent patterns, log forwarding pipelines, structured output, and storage/retention decisions. Getting logging wrong is expensive to fix after the fact. (See [[sources/kubernetes-logging-in-production]])

### Ingress and Networking
Ingress controllers (Nginx, Istio, etc.) handle TLS termination and traffic routing. The choice between TLS termination and TLS passthrough at the gateway has downstream implications for end-to-end encryption, certificate management, and observability. (See [[sources/run-the-istio-ingress-gateway-with-tls-termination-and-tls-passthrough]])

### Host Operating System
The cluster's node OS is often invisible until it isn't. **Talos Linux** represents a minimal, immutable, API-only OS designed specifically for Kubernetes nodes — removes SSH, applies security hardening, enforces reproducibility. (See [[sources/talos-ein-minimal-linux-fuer-kubernetes]])

### Cost and Cluster Sizing
Running Kubernetes in managed cloud environments (AKS, EKS, GKE) can be expensive. Cost-conscious patterns include spot instances, right-sizing, and minimal node pool configurations. (See [[sources/run-kubernetes-in-azure-the-cheap-way]])

### Orchestrator Choice
Kubernetes is not the only option. **Nomad** (HashiCorp) is simpler and better-suited to mixed workloads (containers + raw executables + VMs) in smaller organizations. The choice depends on team size, workload diversity, and tolerance for Kubernetes's operational complexity. (See [[sources/nomad-kubernetes-and-a-pragmatic-look-at-choosing-orchestrators]])

---

## Strategic Context

Kubernetes originated at Google and was open-sourced in 2014. The CNCF (Cloud Native Computing Foundation) now stewards it. The key strategic shift: as managed Kubernetes matures, effort moves from raw mechanics toward **policy, reliability, and developer enablement** — which is precisely where [[topics/platform-engineering]] and [[concepts/internal-developer-platform]] connect. (See [[sources/the-rise-and-future-of-kubernetes-and-open-source-at-google]])

---

## Key Ideas

- Kubernetes is powerful because of its unified control plane — and operationally complex for the same reason
- Practical Kubernetes design depends on surrounding choices: ingress, tenancy, logging, host OS, manifest management
- Managed Kubernetes shifts effort from mechanics to policy and developer enablement
- The gap between "running Kubernetes" and "operating Kubernetes well" is where platform engineering starts

---

## Open Questions

- Which Kubernetes topics deserve deeper first-class pages: ingress patterns, tenancy models, observability, or node OS design?
- How much of the homelab Kubernetes material (K3s, MetalLB, Proxmox) belongs here vs. in [[topics/devops-homelab]]?
- As agentic workloads arrive on clusters, how does Kubernetes resource governance need to evolve?

---

## Sources

- [[sources/introduction-to-kustomize]] — Kustomize manifest customization; per-environment overlays without templating
- [[sources/building-multi-tenant-kubernetes-on-azure-aks]] — Shared cluster design; tenancy and isolation on AKS
- [[sources/kubernetes-logging-in-production]] — Logging architectures; sidecar vs. node-agent patterns
- [[sources/nomad-kubernetes-and-a-pragmatic-look-at-choosing-orchestrators]] — Orchestrator comparison; when Nomad is a better fit
- [[sources/run-kubernetes-in-azure-the-cheap-way]] — Cost-conscious AKS patterns
- [[sources/run-the-istio-ingress-gateway-with-tls-termination-and-tls-passthrough]] — Ingress design; TLS termination vs. passthrough
- [[sources/talos-ein-minimal-linux-fuer-kubernetes]] — Talos as minimal, immutable Kubernetes node OS
- [[sources/the-rise-and-future-of-kubernetes-and-open-source-at-google]] — Strategic history; CNCF governance; cloud-native ecosystem
