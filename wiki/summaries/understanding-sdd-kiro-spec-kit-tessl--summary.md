---
title: "Understanding Spec-Driven Development: Kiro, spec-kit, and Tessl — Summary"
type: summary
source_count: 1
created: 2026-04-29
last_updated: 2026-04-29
tags: [spec-driven-development, coding-agents, thoughtworks, critical-analysis, tool-comparison]
inbound_links: 0
status: complete
source_file: "raw/inbox/Understanding Spec-Driven-Development Kiro, spec-kit, and Tessl.md"
related_pages: ["[[concepts/spec-driven-development]]", "[[topics/ai-software-development]]"]
---

**Author**: Birgitta Böckeler (Thoughtworks) | **Published**: October 15, 2025 | **Source**: [martinfowler.com](https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html)

Böckeler offers a critical analysis of three spec-driven development tools — Kiro (AWS), Spec-kit (GitHub), and Tessl (beta) — organized around a taxonomy of three SDD levels that clarifies what each tool actually achieves. Spec-first means a spec is written before implementation but may be discarded afterward; spec-anchored means the spec is kept for the feature's full lifetime and consulted during evolution; spec-as-source means the spec is the primary artifact and humans never touch generated code. Against this taxonomy: Kiro is lightweight and spec-first, structuring requirements into user stories and acceptance criteria in VS Code — effective for non-trivial features but overkill for small problems, where a single bug becomes four user stories and sixteen acceptance criteria. Spec-kit aspires to spec-anchored but its per-spec git branch structure suggests the spec lifetime matches the change request lifetime rather than the feature lifetime; its planning phase was observed to research existing code and then regenerate it from scratch as new specification. Tessl is the only tool explicitly targeting spec-as-source, with a 1:1 spec-to-code-file mapping and `tessl build` generating all code — still in beta. Böckeler raises four concerns that apply across the category: one workflow does not fit all problem sizes; reviewing many markdown files is frequently more tedious than reviewing code; agents frequently do not follow all instructions, creating a false sense of control; and the model-driven development parallel from the 1990s is instructive — MDD tried to make formal models the source of truth with custom generators, and failed for business applications because abstraction overhead exceeded the benefit. LLMs remove the parseable constraint but add non-determinism: spec-as-source risks the downsides of both inflexibility and unpredictability. The piece closes by noting that the term "spec-driven development" is already semantically diffused — increasingly used as a synonym for "detailed prompt" — and coins the frame "Verschlimmbesserung" (making things worse in the attempt to make them better) as a live risk for the category.

## Key Insights

- The spec-first / spec-anchored / spec-as-source taxonomy is the most useful analytical contribution in the piece: it separates tool ambitions that are frequently conflated, and reveals that most tools claiming to be spec-anchored are functionally spec-first.
- Kiro's proportionality problem is concrete and observable: a small bug producing four user stories and sixteen acceptance criteria is a failure of fit, not a feature — it signals that spec tooling needs problem-size sensitivity.
- Spec-kit's planning-phase behavior — researching existing code, then regenerating it from scratch as new specification — is a direct example of the code duplication failure mode described in `[[summaries/assessing-internal-quality-with-agent--summary]]`, now at the tooling level.
- The MDD parallel is historically grounded and under-discussed in current SDD discourse: the 1990s failure was about abstraction overhead exceeding benefit for real business complexity; LLMs trade parseable constraints for non-determinism, which may shift the failure mode without eliminating it.
- "False sense of control" is the most operationally important concern: if agents frequently do not follow all spec instructions, the spec becomes a confidence artifact rather than a governance artifact, and the human review posture must account for this gap.
- Semantic diffusion of "spec-driven development" into "detailed prompt" is an early warning sign that the category is losing definitional precision, which makes comparative evaluation and adoption decisions harder.
- Cross-reference with the GitHub Spec-kit introduction (`[[summaries/spec-driven-development-spec-kit--summary]]`) for the promotional framing; this piece provides the critical counterweight.

## Related Pages

- [[concepts/spec-driven-development]]
- [[topics/ai-software-development]]
