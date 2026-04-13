---
title: "How to SRE Anything — Summary"
type: summary
source_count: 1
created: 2026-04-13
last_updated: 2026-04-13
tags: [sre, reliability, framework, engineering]
inbound_links: 0
status: complete
related_pages: ["[[concepts/sre-anything-framework]]", "[[topics/devops-homelab]]"]
---

# How to SRE Anything — Summary

**Author**: Jennifer Petoff
**Source**: reliablepgm.com
**Date**: September 2025

## One-Paragraph Summary

SRE principles developed at Google for software reliability generalize to any domain with a reliability requirement — restaurants, customer service, family emergency plans, training programs. Jennifer Petoff's "How to SRE Anything" framework adapts the Service Reliability Hierarchy pyramid (monitoring → incident response → postmortems → testing → capacity planning) as universal questions applicable to any operational context. The framework can even be codified into a Gemini AI Gem for collaborative brainstorming.

## Key Claims

- Reliability is a foundational feature of any product/system — if it's not available, other features don't matter
- SRE is about appropriate level of reliability and balancing competing concerns, not 100% perfection
- Core questions transfer to any domain: What can you observe? What do you do when things go wrong? How will you learn? How can you pilot? How will you scale?
- Blameless postmortems, toil reduction, and DiRT testing are universal operational practices
- AI agents (Gemini Gems) can be trained to apply the framework interactively

## Example: Family Emergency Plan

Monitoring = Lifeline device + friends with line of sight
Incident Response = Clear on-call structure; playbooks; escalation
Postmortems = Retrospective after DiRT tests
Pilots = Test HIPAA access before a crisis
Capacity Planning = Know your support network; avoid SPoFs

## Filing Status

- [x] All sections complete
