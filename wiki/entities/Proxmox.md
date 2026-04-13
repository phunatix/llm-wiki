---
title: Proxmox VE
type: entity
source_count: 2
created: 2026-04-13
last_updated: 2026-04-13
tags: [homelab, virtualization, devops, infrastructure]
inbound_links: 0
status: complete
related_pages: ["[[topics/devops-homelab]]", "[[summaries/k3s-metallb-proxmox--summary]]", "[[summaries/proxmox-influxdb-grafana--summary]]"]
---

# Proxmox VE

**Category**: Software (Open-source Hypervisor / Virtualization Platform)

**Quick Summary**: Open-source hypervisor platform for running VMs and containers; the standard homelab virtualization layer; has built-in metrics export to InfluxDB.

## Overview

Proxmox Virtual Environment (PVE) is a Debian-based open-source server virtualization platform. It supports both KVM (full virtualization) and LXC (containers), managed through a web UI. Common in homelab setups as a base layer for running Kubernetes clusters, monitoring stacks, and other services.

## Key Features

- Web-based management UI
- KVM virtual machines + LXC containers
- Built-in **external metric server** (sends metrics to InfluxDB or Graphite)
- Cloud-init support for VM templates
- Clustering support

## Homelab Integration Patterns

**K3s cluster on Proxmox:**
- Create 3x Ubuntu 22.04 VMs from cloud-init template
- Static IPs via netplan
- Install K3s master (disable Traefik + ServiceLB for MetalLB use)
- Add worker nodes with master token
- Install MetalLB via Helm for LoadBalancer services

**Monitoring via Proxmox metric server:**
- Configure: Datacenter → Metric Server → Add InfluxDB (use HTTP, not UDP)
- InfluxDB receives metrics (CPU, memory, storage, VM uptime) per host/VM
- Grafana connects to InfluxDB with InfluxQL (not Flux — Flux being deprecated)
- Dashboard template available: [Grafana ID 22482](https://grafana.com/grafana/dashboards/22482)

## Key Notes

- Proxmox metric server uses `proxmox` as default bucket name in InfluxDB
- UDP protocol: cannot override org/bucket names — use HTTP
- Metrics include per-host and per-VM data; `nodename` tag distinguishes PVE hosts from VMs
- InfluxQL preferred over Flux for new Grafana integrations (Flux entering maintenance mode)

## See Also

- [[topics/devops-homelab]]
- [[summaries/k3s-metallb-proxmox--summary]]
- [[summaries/proxmox-influxdb-grafana--summary]]

## Sources

- [[summaries/k3s-metallb-proxmox--summary]]: K3s cluster deployment on Proxmox VMs
- [[summaries/proxmox-influxdb-grafana--summary]]: Metrics integration with InfluxDB and Grafana
