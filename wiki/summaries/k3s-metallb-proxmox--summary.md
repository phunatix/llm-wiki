---
title: "K3s + MetalLB on Proxmox — Summary"
type: summary
source_count: 1
created: 2026-04-13
last_updated: 2026-04-13
tags: [kubernetes, k3s, metallb, proxmox, homelab]
inbound_links: 0
status: complete
related_pages: ["[[entities/Proxmox]]", "[[topics/devops-homelab]]"]
---

# K3s + MetalLB on Proxmox — Summary

**Author**: Ruben Dario Coria
**Source**: blog.chicho.com.ar
**Date**: February 2024

## One-Paragraph Summary

A step-by-step guide for deploying a bare-metal Kubernetes cluster using K3s on Proxmox VMs (Ubuntu 22.04, cloud-init), with MetalLB providing LoadBalancer functionality. Three VMs: one master, two workers. K3s installed with Traefik and ServiceLB disabled (to use MetalLB + Nginx Ingress instead). MetalLB configured via Helm with a Layer 2 IP address pool.

## Setup Summary

1. **Proxmox VMs**: 3x Ubuntu 22.04 from cloud-init template; static IPs via netplan
2. **K3s Master**: `curl -sfL https://get.k3s.io | INSTALL_K3S_EXEC="server --disable traefik --disable servicelb" sh -`
3. **K3s Workers**: Join with master token via `K3S_URL` + `K3S_TOKEN`
4. **Remote kubectl**: Copy `/etc/rancher/k3s/k3s.yaml` to `~/.kube/config`; update IP from 127.0.0.1
5. **MetalLB via Helm**: Add repo → create namespace → install → configure IPAddressPool + L2Advertisement

## Key Notes

- Disable kippler-db (K3s default ServiceLB) and Traefik when using MetalLB + Nginx Ingress
- MetalLB Layer 2 mode: assign IP range from your router's reserved pool
- Test: `kubectl create deploy nginx --image=nginx` + `expose as LoadBalancer` → should get external IP from MetalLB pool

## Filing Status

- [x] All sections complete
