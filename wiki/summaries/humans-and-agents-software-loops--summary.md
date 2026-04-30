---
title: "Humans and Agents in Software Engineering Loops — Summary"
type: summary
source_count: 1
created: 2026-04-29
last_updated: 2026-04-29
tags: [ai-agents, coding-agents, thoughtworks, developer-workflow, harness-engineering]
inbound_links: 0
status: complete
source_file: "raw/inbox/Humans and Agents in Software Engineering Loops.md"
related_pages: ["[[concepts/harness-engineering]]", "[[concepts/agentic-development-loop]]", "[[topics/ai-software-development]]"]
---

**Author**: Kief Morris (Thoughtworks) | **Published**: 2026-04-29 (no published date in source) | **Source**: [martinfowler.com](https://martinfowler.com/articles/exploring-gen-ai/humans-and-agents.html)

Morris introduces a two-loop model for reasoning about human and agent roles in software engineering: the "why loop," which iterates between an idea and working software and is inherently human territory because it encodes what we actually care about, and the "how loop," which iterates over intermediate artefacts — specifications, code, tests — and operates at multiple levels from feature to story to code. Three human postures are defined relative to these loops. Outside the loop (vibe coding) places humans in the why loop and agents in the how loop — appealing because the why loop is where the value lives, but the risk is silent quality degradation with no mechanism to course-correct. In the loop places humans closely inside the innermost code-generation loop, inspecting every artefact — but agents produce faster than humans can inspect, making this a bottleneck. On the loop is the proposed discipline: humans build and maintain the harness that causes agents to self-regulate, with the key distinction being that in-the-loop corrects a bad artefact while on-the-loop changes the harness that produced it. Morris then describes an "agentic flywheel" — a self-improving system where agents are directed to manage and improve the harness itself using pipeline data and production signals, auto-approving high-confidence improvements — and argues this state of productive automation is only reachable via engineered discipline, not vibe coding.

## Key Insights

- The why/how loop distinction clarifies what "human oversight" should actually mean: humans belong in the why loop by nature, and the question is how much of the how loop they can safely delegate and to what degree.
- The three postures (outside, in, on the loop) are not equally viable at scale: outside lacks correction mechanisms; in is rate-limited by human inspection speed; on is the only posture that scales while preserving quality control.
- The sharpest formulation in the piece: "the difference between in the loop and on the loop is most visible in what we do when we're not satisfied: in-the-loop fixes the artefact, on-the-loop changes the harness that produced the artefact." This reframes code review as harness design.
- The agentic flywheel — agents improving the harness that governs agents — is the logical endpoint of on-the-loop thinking; it is a self-improving system with engineered, not accidental, properties.
- Vibe coding is not rejected as unproductive but as architecturally fragile: it works until quality degradation compounds invisibly, at which point there is no systematic way to diagnose or correct.
- This framework complements the Doernenburg piece (`[[summaries/assessing-internal-quality-with-agent--summary]]`): internal quality failures are exactly the kind of silent degradation that the on-the-loop posture is designed to surface and correct through harness feedback rather than artefact-level intervention.

## Related Pages

- [[concepts/harness-engineering]]
- [[concepts/agentic-development-loop]]
- [[topics/ai-software-development]]
