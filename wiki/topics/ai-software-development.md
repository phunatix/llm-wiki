---
title: AI & Software Development
type: topic
source_count: 5
created: 2026-04-13
last_updated: 2026-04-23
tags: [ai, coding-agents, developer-tools, llm, developer-productivity]
inbound_links: 0
status: complete
related_pages: ["[[concepts/ai-developer-stages]]", "[[concepts/agentic-coding-risks]]", "[[entities/Thomas-Dohmke]]", "[[entities/LM-Studio]]", "[[concepts/agentic-development-loop]]"]
---

# AI & Software Development

**Scope**: How AI tools and coding agents are transforming software development practice, developer identity, skills, and workflows — including both the opportunities and the serious risks of uncritical adoption.

**Overview**: A profound shift is underway. AI coding tools are moving developers from writing code toward orchestrating, verifying, and guiding AI agents. This brings speed and ambition, but also compounding errors, loss of architectural control, and codebase brittleness when adopted without discipline.

## What's Included

- AI adoption stages for developers
- Coding agent workflows (Cursor, Roo Code, Claude Code, etc.)
- Self-hosted AI coding setups
- Risks of agentic coding
- The evolving developer identity and skills
- AI's impact on developer education
- Europe's AI dependency and geopolitical risk

## Core Concepts

- [[concepts/ai-developer-stages]]: The four-stage progression from AI Skeptic → AI Strategist
- [[concepts/agentic-coding-risks]]: Compounding errors, merchant-of-complexity problem, low recall
- [[concepts/delegation-and-verification]]: The new developer role — delegate to agents, verify output
- [[concepts/agentic-development-loop]]: The friction-removal loop; Theory of Constraints applied to dev workflow; implementer → agent manager identity shift

## Key Entities

- [[entities/Thomas-Dohmke]]: GitHub CEO; research on developer AI adoption patterns
- [[entities/LM-Studio]]: Local LLM serving tool enabling self-hosted AI coding
- GitHub Copilot / Claude Code / Cursor / Roo Code: AI coding tools driving adoption

## Landscape Map

```
AI Coding Tool Spectrum
├── Completions (GitHub Copilot, Cursor tab)
├── Chat (ChatGPT, Claude.ai)
├── IDE agents (Cursor, Claude Code, Roo Code)
└── Autonomous agents (multi-agent orchestration)

Risk / Discipline Required: LOW ────────────────────────────── HIGH
Control:                    HIGH ────────────────────────────── LOW
Speed:                      LOW  ────────────────────────────── HIGH
```

## Key Debates

- **Speed vs. discipline**: Agents produce code fast, but without discipline the codebase becomes unmaintainable within weeks
- **Replace or augment?**: Will AI replace developers (reduce headcount) or expand their ambition (do more with same team)?
- **Delegation ceiling**: How much can you safely delegate before you lose understanding of what you built?
- **Open-source vs. proprietary models**: Chinese open-weight models (DeepSeek, Qwen, Kimi) vs. US closed models — affects self-hosting viability

## Key Insights

- The best developers using AI are moving from "code producers" to "code directors" — architecture, verification, delegation
- 50% of interviewed AI-heavy developers believe 90% AI-written code is realistic within 2 years
- The failure mode is not using AI — it's removing yourself from the loop entirely
- Good agent tasks: well-scoped, self-evaluable, non-critical, reversible
- Bad agent tasks: architecture decisions, anything requiring full-codebase context
- Self-hosted AI coding is increasingly viable (LM Studio + Qwen3-Coder + Roo Code)
- Europe's 70%+ dependency on US cloud for AI is a structural vulnerability
- As agent autonomy increases, platform and governance concerns become inseparable from developer workflow concerns — a developer choosing an AI tool is now also making an infrastructure and security decision

## Recent Developments

- **2025-06**: MCP crosses into mainstream — OpenAI and Google Deepmind adopt it; all major LLM providers now on board; API-first companies racing to expose services as MCP tools; MCP becoming a core layer of how APIs are exposed and consumed by agents
- **2026-04**: German IT salary data shows AI roles (~77K€ median) not yet commanding premium over general developers
- **2026-03**: Neil Kakkar (Tano) documents six weeks of Claude Code use; Theory of Constraints framing; 5 parallel agent worktrees; identity shift from implementer to manager
- **2026-03**: Growing reports of production instability from over-delegated agent coding
- **2026**: AWS alleged AI-caused outage followed by 90-day "code quality reset"
- **2025-08**: Self-hosted AI coding stack (LM Studio + Qwen3-Coder + Roo Code) reaches practical usability

## See Also

- [[topics/platform-engineering]]: AI is creating new demands on internal developer platforms
- [[topics/personal-knowledge-management]]: AI is transforming PKM just as it is coding
- [[concepts/sre-anything-framework]]: SRE principles apply to evaluating AI tooling risks

## Sources by Relevance

- [[summaries/developers-reinvented--summary]]: Most systematic treatment of AI adoption stages and skills
- [[summaries/thoughts-on-slowing-down--summary]]: Strongest critique of uncritical agentic adoption
- [[summaries/productive-with-claude-code-summary]]: Practitioner account; Theory of Constraints + friction-removal loop; 6 weeks at Tano
- [[summaries/self-hosted-ai-coding--summary]]: Practical guide to self-hosted AI coding stack
- [[summaries/us-cuts-off-tech-to-europe--summary]]: Geopolitical context for AI tool dependency
