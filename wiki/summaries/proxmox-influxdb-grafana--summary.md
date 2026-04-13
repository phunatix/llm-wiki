---
title: "Proxmox + InfluxDB + Grafana Monitoring — Summary"
type: summary
source_count: 1
created: 2026-04-13
last_updated: 2026-04-13
tags: [proxmox, influxdb, grafana, monitoring, homelab]
inbound_links: 0
status: complete
related_pages: ["[[entities/Proxmox]]", "[[topics/devops-homelab]]"]
---

# Proxmox + InfluxDB + Grafana Monitoring — Summary

**Author**: Rudi Martinsen
**Source**: rudimartinsen.com
**Date**: December 2024

## One-Paragraph Summary

How to use Proxmox VE's built-in external metric server to push metrics to InfluxDB 2.7, then visualize them in Grafana using InfluxQL (not Flux, which is being deprecated). InfluxDB needs a bucket and write token; Proxmox needs the metric server configured with HTTP protocol and those credentials; Grafana connects via InfluxQL datasource with auth header. Grafana Dashboard ID 22482 provides a ready-made template.

## Setup Summary

**InfluxDB**:
1. Create bucket named `proxmox`
2. Create write token (for Proxmox) → copy immediately (not retrievable after)
3. Create read token (for Grafana)

**Proxmox**:
- Datacenter → Metric Server → Add InfluxDB
- Protocol: HTTP (UDP doesn't allow org/bucket override)
- Specify: host, port, org, bucket name, token

**Grafana**:
- Add InfluxDB datasource with InfluxQL query language
- Auth header: `Authorization: Token <token>`
- Database: `proxmox` (your bucket name)
- Method: GET

## Key Notes

- Flux query language entering "maintenance mode" — use InfluxQL for new Grafana integrations
- `nodename` tag identifies PVE hosts; `vmid` tag (regex match on digits) identifies VMs
- Dashboard template: grafana.com/grafana/dashboards/22482

## Filing Status

- [x] All sections complete
