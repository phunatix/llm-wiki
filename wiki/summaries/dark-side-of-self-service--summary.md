---
title: "Dark Side of Self-Service — Summary"
type: summary
source_count: 1
created: 2026-04-13
last_updated: 2026-04-13
tags: [platform-engineering, devops, developer-experience]
inbound_links: 0
status: complete
related_pages: ["[[concepts/cognitive-load]]", "[[concepts/golden-paths]]", "[[concepts/developer-self-service]]", "[[entities/Humanitec]]", "[[entities/Kaspar-von-Grunberg]]"]
---

# Dark Side of Self-Service — Summary

**Author**: Kaspar von Grünberg (CEO, Humanitec)
**Source**: humanitec.com/blog/what-developer-self-service-shouldnt-look-like
**Date**: August 2021

## One-Paragraph Summary

Developer self-service is often done spectacularly wrong, in two opposite directions: "throwing everything" at developers (complex Kubernetes/Terraform/Argo stacks with no training or abstraction) or "taking it all from them" (opaque platforms developers can't understand or extend). Both fail. The right model is [[concepts/golden-paths]] — abstractions that developers understand, can escape from, and chose to follow because they see value. The key metric is [[concepts/cognitive-load]], and the key mechanism is communication.

## Key Claims

- Self-service is often abused: ops teams build complex "cool" stacks, then throw them at developers under the "you build it, you run it" banner without proper training
- The opposite abuse: central platform teams build black-box abstractions so opaque that developers lose trust and abandon the platform
- Division of labor is inevitable at scale — "To run 1,000 services around Kubernetes, you shouldn't need 1,000 Kubernetes experts"
- 97% of developers follow a golden path once established, if they understand why it exists
- Communication is the single most important component: treat developers as users; iterate with them

## Research Data Point

From Humanitec analysis of 1,856 engineering teams:
- 21.2%: True "you build it, you run it"
- 32.2%: Traditional throw-over-the-fence (ops separate)
- 44.6%: Walls torn down but developers overwhelmed

## Entities Mentioned

- [[entities/Humanitec]]: Author's company; Platform Orchestrator
- [[entities/Kaspar-von-Grunberg]]: Author
- Jason Warner (GitHub CTO): Referenced; GitHub's golden paths approach
- Aaron Erickson (Salesforce): "1,000 services → shouldn't need 1,000 Kubernetes experts" quote

## Filing Status

- [x] Entities updated
- [x] Concepts updated
- [x] Topic page updated
- [x] Index updated
- [x] Log updated
