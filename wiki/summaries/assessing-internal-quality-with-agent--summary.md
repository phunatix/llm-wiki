---
title: "Assessing Internal Quality While Coding with an Agent — Summary"
type: summary
source_count: 1
created: 2026-04-29
last_updated: 2026-04-29
tags: [ai-agents, code-quality, thoughtworks, software-engineering, swift]
inbound_links: 0
status: complete
source_file: "raw/inbox/Assessing internal quality while coding with an agent.md"
related_pages: ["[[concepts/agentic-coding-risks]]", "[[concepts/harness-engineering]]", "[[topics/ai-software-development]]"]
---

**Author**: Erik Doernenburg (Thoughtworks) | **Published**: January 27, 2026 | **Source**: [martinfowler.com](https://martinfowler.com/articles/exploring-gen-ai/ccmenu-quality.html)

A practitioner account of adding GitLab support to CCMenu (a Swift Mac app) using Claude Code with Sonnet 4.5, focused specifically on whether the agent maintained internal code quality — not just whether the output compiled and worked. Doernenburg documents four distinct quality failures: the agent declared API wrapper functions with non-optional `String` parameters when `String?` was semantically correct, then when the compiler surfaced errors, spread `?? ""` across every call site rather than fixing the signature — producing compiling, functional code that had destroyed its own semantic intent; it proposed an unnecessary cache for a problem that required none; it duplicated existing URL construction logic while omitting functionality already present in the codebase; and it hallucinated the existence of a GitLab API response field, requiring extended correction. In every case the code compiled and the feature worked. The conclusion is that internal quality degradation under agentic coding is systematic, invisible to automated checks, and will not surface until the codebase becomes difficult to maintain or extend — making continuous human oversight of code quality not optional but essential. Claude Code with Sonnet 4.5 is noted as meaningfully better than Windsurf with Sonnet 3.5, but the pattern of quality erosion was consistent across both.

## Key Insights

- Agents optimize for compilation and test passage, not semantic correctness — a function signature error becomes `?? ""` spread at every call site rather than a fix at the source, a pattern that is architecturally corrosive.
- Internal quality failures are invisible to automated checks: the code compiled, the tests passed, the feature worked. Degradation accumulates silently.
- Three distinct failure modes observed in one session: unnecessary abstraction (cache), code duplication without feature parity, and API hallucination. None were caught by the compiler.
- Human oversight must be calibrated to code structure and intent, not just output correctness — reviewers who only check "does it work" will miss all four failure patterns described.
- Model quality matters: Sonnet 4.5 via Claude Code outperformed Sonnet 3.5 via Windsurf, suggesting both the model and the agentic harness affect internal quality outcomes.
- The practical implication for teams: define explicit code quality criteria in the harness (see `[[concepts/harness-engineering]]`) and treat code review for agentic output as a distinct, non-negotiable discipline.

## Related Pages

- [[concepts/agentic-coding-risks]]
- [[concepts/harness-engineering]]
- [[topics/ai-software-development]]
