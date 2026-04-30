---
title: '"SRE Anything" Framework'
type: concept
source_count: 2
created: 2026-04-13
last_updated: 2026-04-13
tags: [sre, reliability, framework, engineering]
inbound_links: 0
status: complete
related_pages: ["[[topics/devops-homelab]]", "[[topics/platform-engineering]]"]
---

# "SRE Anything" Framework

**Domain**: Site Reliability Engineering / Operational Excellence

**One-line definition**: A generalization of Google's SRE Service Reliability Hierarchy to any domain — software, restaurants, family emergency plans, training programs — providing a structured way to think about reliability for any "system."

## Definition

Developed by Jennifer Petoff (SRE + Program Management at Google), the "How to SRE Anything" framework applies the SRE reliability hierarchy to non-software domains. The key insight: reliability principles (monitoring, incident response, postmortems, testing/pilots, capacity planning) are universal to any system that needs to run reliably.

## The Three Inputs

- **$TheDomain**: The context (software, restaurant, customer service, family emergency)
- **$TheThing**: What you are trying to build or achieve
- **$MeansToGetThere**: How you will achieve it reliably

## The Adapted Reliability Hierarchy

| Level | SRE Original | Generalized Question |
|-------|-------------|---------------------|
| **Aspiration** | Product | Well-Oiled Machine |
| 6 | Development | $TheThing (what are you building?) |
| 5 | Capacity Planning | How will you scale? |
| 4 | Testing & Release | How can you pilot? |
| 3 | Postmortem/RCA | How will you learn from failure? |
| 2 | Incident Response | What do you do when things go wrong? |
| 1 | Monitoring | What can you observe? |

## Example: Family Emergency Plan

| Level | Concrete Application |
|-------|---------------------|
| Well-Oiled Machine | Family seamlessly caring for loved one when you can't |
| $TheThing | Reliable support available; information flows in crisis |
| Scale | Know who can help; not doing it alone |
| Pilot | Test HIPAA release access before a crisis |
| Learn | Retrospective after DiRT test |
| Incident Response | Clear on-call; playbook; escalation path |
| Monitor | Lifeline device; friends with line of sight |

## SRE Principles That Transfer

- **Blameless postmortems**: Focus on system failures, not individual blame
- **Toil reduction**: Automate repetitive work to scale operations super-linearly
- **DiRT testing**: Disaster Recovery Testing — stress test your plans before you need them
- **SPoF avoidance**: Single Points of Failure apply everywhere, not just software

## SRE as a Discipline

Beyond the "SRE Anything" framework, SRE is a distinct engineering discipline with its own principles:

- **Reliability is a product property**: It must be balanced against velocity, cost, and effort — not maximized in isolation. An obsession with 100% uptime at the expense of development speed is anti-SRE
- **Toil reduction**: Repetitive, automatable operational work is "toil"; SRE's goal is to reduce toil so engineers can focus on systemic improvements rather than repetitive manual tasks
- **Blameless postmortems**: When things fail, the focus is on system and process failures — not individuals. This is a cultural commitment, not just a process
- **Observability**: You can only improve what you can see. Monitoring, alerting, and tracing are foundational — not optional add-ons
- **SLOs over SLAs**: Service Level Objectives (internal targets) are preferred over contractual SLAs because they create space for iteration without breach — the error budget model

SREs are generalist engineers who deliberately work close to production — debugging production incidents, designing for failure, and building automation that reduces their own operational burden.

*Source: [[sources/site-reliability-engineers-we-solve-cooler-problems]] — Google Careers; "We solve cooler problems" framing; production-close generalist engineering role*

## AI Application

The framework can be codified into a Gemini Gem (AI agent) that walks users through applying the hierarchy to their domain, one level at a time.

## See Also

- [[topics/devops-homelab]]
- [[topics/platform-engineering]]

## Sources

- [[summaries/sre-anything--summary]]
- [[sources/site-reliability-engineers-we-solve-cooler-problems]] — Google Careers; the SRE role as production-close generalist engineer; "we solve cooler problems" framing
