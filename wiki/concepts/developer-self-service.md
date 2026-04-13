---
title: Developer Self-Service
type: concept
source_count: 2
created: 2026-04-13
last_updated: 2026-04-13
tags: [platform-engineering, devops, developer-experience]
inbound_links: 0
status: complete
related_pages: ["[[concepts/cognitive-load]]", "[[concepts/golden-paths]]", "[[concepts/internal-developer-platform]]"]
---

# Developer Self-Service

**Domain**: Platform Engineering / DevOps

**One-line definition**: The ability of developers to independently provision infrastructure, deploy applications, and manage operations without waiting for a separate ops team — when done correctly.

## Definition

Developer self-service is the realization of "you build it, you run it" at scale. Rather than throwing work over the fence to operations, developers can serve themselves through platform tooling. The critical insight from [[entities/Humanitec]] research is that **self-service is often done spectacularly wrong**, in two opposite directions.

## The Division of Labor Reality

> "Service ownership is a good idea in theory, but in practice... if developers have to run all the ops for their services, you do not have any economies of scale. To run 1,000 different services around Kubernetes, you shouldn't need 1,000 Kubernetes experts." — Aaron Erickson, Salesforce IDP

At enterprise scale, some division of labor is inevitable and correct. The question is not "should ops exist?" but "where is the optimal handoff point?"

## The Research Numbers

From Humanitec's analysis of 1,856 engineering teams:
- **21.2%**: True "you build it, you run it" 
- **32.2%**: Traditional throw-over-the-fence (ops separate from dev)
- **44.6%**: Walls torn down but developers overwhelmed — senior devs informally take over ops role

The 44.6% case often isn't better than traditional split — it's unplanned, uncompensated ops work.

## Keys to Success

1. **Communicate with developers**: What do they want to own? What do they want abstracted?
2. **Build golden paths**: See [[concepts/golden-paths]]
3. **Treat developers as users**: Feedback loops, iteration, respect for their time
4. **Explain the social contract**: Why the golden path benefits everyone

## See Also

- [[concepts/cognitive-load]]
- [[concepts/golden-paths]]
- [[concepts/internal-developer-platform]]
- [[topics/platform-engineering]]

## Sources

- [[summaries/dark-side-of-self-service--summary]]
- [[summaries/whats-the-future-of-platform-engineering--summary]]
