---
title: "Thoughts on Slowing the F*ck Down — Summary"
type: summary
source_count: 1
created: 2026-04-13
last_updated: 2026-04-13
tags: [ai, coding-agents, software-quality, opinion]
inbound_links: 0
status: complete
related_pages: ["[[concepts/agentic-coding-risks]]", "[[topics/ai-software-development]]"]
---

# Thoughts on Slowing the F*ck Down — Summary

**Author**: Mario Zechner
**Source**: mariozechner.at
**Date**: March 2026

## One-Paragraph Summary

A candid critique of uncritical agentic coding adoption. After one year of coding agents in production, the author documents the systemic risks: software is becoming increasingly brittle, codebases coded into corners in weeks, agentic search has low recall, agents are merchants of complexity, and errors compound at rates humans can't sustain. The prescription: slow down, write architecture by hand, stay in the code, set daily code-generation limits in line with your ability to review.

## Key Claims

- Agents make errors that compound with no human pain signal to trigger cleanup
- Unlike humans, agents don't learn from repeated mistakes — same booboos recur indefinitely
- Agents have no bottleneck — they introduce errors at an unsustainable rate
- Agents see only local context; complex codebases exceed their recall capacity
- Agents are trained on bad architectural patterns; they produce complexity without judgment
- Production evidence: AWS alleged AI-caused outage; Microsoft Windows quality concerns; "90-day reset" at Amazon
- Companies claiming 100% AI-written code consistently produce the worst software

## Good vs. Bad Agent Tasks

**Safe**: Scoped, self-evaluable, non-critical, non-architectural ("boring stuff")
**Dangerous**: Architecture, API design, anything requiring full-codebase context

## The Prescription

> "Anything that defines the gestalt of your system — architecture, API — write it by hand. Be in the code. Slowing the fuck down and suffering some friction is what allows you to learn and grow."

## Contradictions

- [[summaries/developers-reinvented--summary]] presents a more optimistic view of agentic Stage 4 development
- The cautionary perspective here is supported by empirical production evidence (AWS, Microsoft) that Dohmke's optimism doesn't address

## Filing Status

- [x] All sections complete
