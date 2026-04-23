---
title: DevOps & Homelab
type: topic
source_count: 5
created: 2026-04-13
last_updated: 2026-04-23
tags: [devops, homelab, kubernetes, proxmox, monitoring, sre, cost-optimization, ai-agents]
inbound_links: 0
status: complete
related_pages: ["[[entities/Proxmox]]", "[[concepts/sre-anything-framework]]", "[[entities/LM-Studio]]", "[[entities/Heinzel]]", "[[concepts/frugal-architecture]]"]
---

# DevOps & Homelab

**Scope**: Practical DevOps, infrastructure, and homelab topics — Kubernetes, monitoring, and related tooling.

## Core Concepts

- [[concepts/sre-anything-framework]]: The SRE reliability hierarchy generalized to any domain
- [[concepts/frugal-architecture]]: Werner Vogels' 7 laws for cost-aware cloud architecture; frugality = maximizing value, not minimizing cost
- K3s: Lightweight Kubernetes distribution for homelab and edge
- MetalLB: Load balancer for bare-metal Kubernetes clusters
- InfluxDB + Grafana: The standard open-source monitoring stack

## Key Entities

- [[entities/Proxmox]]: Open-source hypervisor; platform for homelab virtualization
- [[entities/Heinzel]]: Open-source AI sysadmin assistant; ~140 KB Markdown ruleset for terminal AI agents; anti-hallucination design, dry-run-first, prompt injection protection

## Key How-Tos

- [[summaries/k3s-metallb-proxmox--summary]]: Setting up K3s + MetalLB on Proxmox VMs
- [[summaries/proxmox-influxdb-grafana--summary]]: Proxmox metrics → InfluxDB → Grafana dashboards
- [[summaries/heinzel-sysadmin-summary]]: Heinzel AI sysadmin tool overview; architecture, safety, team workflow

## Architecture Pattern (Proxmox Homelab)

```
Proxmox Host
├── VM: K3s Master (Ubuntu 22.04)
├── VM: K3s Worker 1 (Ubuntu 22.04)
├── VM: K3s Worker 2 (Ubuntu 22.04)
│   └── MetalLB (LoadBalancer, Layer 2)
├── VM: InfluxDB (metrics storage)
└── VM: Grafana (visualization)
         ↑
   Proxmox built-in metric server → InfluxDB
```

## Key Insights

- K3s disables Traefik and ServiceLB by default when using MetalLB — `--disable traefik --disable servicelb`
- InfluxDB Flux query language is being deprecated; prefer InfluxQL for new Grafana integrations
- Proxmox metric server defaults to UDP — use HTTP to override org/bucket names in InfluxDB
- MetalLB Layer 2 mode is simpler for homelab (no BGP router needed)
- SRE principles generalize beyond software to any operational domain

## See Also

- [[topics/platform-engineering]]: Related DevOps principles at organizational scale
- [[concepts/sre-anything-framework]]: The meta-framework for applying SRE thinking
- [[concepts/cloud-sovereignty]]: Sovereignty trade-offs intersect with Frugal Architecture Law 3

## Sources by Relevance

- [[summaries/k3s-metallb-proxmox--summary]]: K3s cluster on Proxmox setup guide
- [[summaries/proxmox-influxdb-grafana--summary]]: Monitoring integration
- [[summaries/sre-anything--summary]]: SRE framework applied broadly
- [[summaries/frugal-architecture-summary]]: AWS Well-Architected + Frugal Architect 7 laws
- [[summaries/heinzel-sysadmin-summary]]: AI-assisted server administration with guardrails
