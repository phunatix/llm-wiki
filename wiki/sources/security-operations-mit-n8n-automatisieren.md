---
title: Security Operations mit n8n automatisieren
type: source
status: active
created: 2026-04-10
updated: 2026-04-10
source_files:
  - raw/sources/Security Operations mit n8n automatisieren.md
tags:
  - source
  - security
  - automation
  - n8n
---

# Summary

This source is a practical tutorial on using n8n to automate security operations workflows. It covers two example flows: threat-intelligence enrichment of suspicious IPs and event-driven handling of Wazuh alerts with LLM-generated HTML recommendations sent by email.

# Key Takeaways

- n8n can automate repetitive SOC work such as enrichment, reporting, and notification.
- The tutorial combines classic integrations with LLM-based alarm interpretation and recommendation generation.
- The article is notable for its concrete workflow composition: webhooks, code nodes, parallel API calls, Wazuh integration, and AI model invocation.

# Relationships

- Related to [Site Reliability Engineering](../concepts/site-reliability-engineering.md) through operational automation.
- Related to [AI-Assisted Software Development](../concepts/ai-assisted-software-development.md) through operational AI use.

# Open Questions

- Should the wiki eventually distinguish between observability automation, incident response automation, and broader agentic operations?
