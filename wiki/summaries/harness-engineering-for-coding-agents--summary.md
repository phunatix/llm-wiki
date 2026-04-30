---
title: "Harness Engineering for Coding Agent Users — Summary"
type: summary
source_count: 1
created: 2026-04-29
last_updated: 2026-04-29
tags: [harness-engineering, coding-agents, thoughtworks, quality, feedback-loops]
inbound_links: 0
status: complete
source_file: "raw/inbox/Harness engineering for coding agent users.md"
related_pages: ["[[concepts/harness-engineering]]", "[[concepts/agentic-coding-risks]]", "[[topics/ai-software-development]]"]
---

# Harness Engineering for Coding Agent Users — Summary

**Author**: Thoughtworks (Martin Fowler's blog)
**Published**: April 2, 2026
**Source**: [martinfowler.com](https://martinfowler.com/articles/harness-engineering/)

---

## One-Paragraph Summary

Harness engineering is the emerging practice of building and maintaining a system of *feedforward guides* (context fed to agents before they act) and *feedback sensors* (signals that let agents evaluate and correct their own output) to regulate what coding agents produce at scale. The framework distinguishes two sensor types: **computational** (deterministic, cheap — linters, type checkers, test suites, architectural drift detectors) and **inferential** (LLM-based, expensive — catching semantic problems like redundant tests or over-engineering, but probabilistically). Three regulation dimensions matter: **maintainability** (most tractable, rich pre-existing tooling), **architecture fitness** (fitness functions, performance sensors), and **behavior** (functional correctness — still largely unsolved; agent-generated tests are necessary but insufficient). The ultimate vision is harness templates — bundles of guides and sensors for common service topologies — analogous to service templates, but with harder versioning and coherence challenges.

---

## Key Insights

- **Sensors catch structurally, not semantically**: Computational sensors reliably catch duplicate code, complexity, missing coverage, architectural drift, style violations. Inferential (LLM) sensors can partially catch semantically duplicate code, redundant tests, brute-force fixes — but expensively and probabilistically. Neither reliably catches misdiagnosis, overengineering, or misunderstood instructions.
- **The behavior harness is the unsolved problem**: Most teams using high-autonomy agents rely on AI-generated test suites + manual testing for functional correctness. This puts too much faith in AI-generated tests. The approved-fixtures pattern helps selectively but is not a wholesale answer.
- **Harnessability is a design property**: Strongly typed languages, clear module boundaries, and abstraction-heavy frameworks all improve harnessability. Legacy codebases face the hardest problem — harnesses are most needed where they're hardest to build (high debt, poor structure).
- **Real precedents exist**: OpenAI documented their harness (layered architecture enforced by linters + recurring "garbage collection" for drift), Stripe's Minions team describes shift-feedback-left with pre-push hook linters, and Thoughtworks teams are using "janitor armies" of agents to increase code and API quality.
- **Open question on harness coherence**: As harnesses grow, keeping guides and sensors in sync — not contradicting each other — is an unsolved tooling problem. Coverage and quality evaluation for a harness (analogous to code coverage for tests) is also needed.

---

## Related Pages

- [[concepts/harness-engineering]] — Full concept page; all framework details incorporated here
- [[concepts/agentic-coding-risks]] — The risks that harness engineering addresses
- [[topics/ai-software-development]] — Broader context
