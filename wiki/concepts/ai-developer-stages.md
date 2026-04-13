---
title: AI Developer Adoption Stages
type: concept
source_count: 1
created: 2026-04-13
last_updated: 2026-04-13
tags: [ai, software-development, developer-skills]
inbound_links: 0
status: complete
related_pages: ["[[entities/Thomas-Dohmke]]", "[[concepts/agentic-coding-risks]]", "[[topics/ai-software-development]]"]
---

# AI Developer Adoption Stages

**Domain**: AI & Software Development

**One-line definition**: A four-stage model describing how developers progress from AI skepticism to treating AI agents as powerful creative partners — based on interviews with 22 AI-heavy developers by GitHub CEO Thomas Dohmke.

## The Four Stages

### Stage 1: AI Skeptic
- Dabbling with AI for small tasks; code completions only
- Low tolerance for iteration and errors
- Common reaction: "Pretty cool, but gimmicky"
- Key hurdle: Shedding expectation for one-shot success

### Stage 2: AI Explorer
- Using AI for debugging, boilerplate, and snippets
- Copy-pasting from browser-based LLMs
- Starting to understand AI's limitations
- Beginning to iterate and restart rather than push through bad outputs

### Stage 3: AI Collaborator
- Actively co-creating with AI in IDE
- Multi-step tasks, multi-file changes
- Developing "context engineering intuition"
- Habits: prompt-for-plan first, curate agent rules, switch between models
- Joining internal demos to share effective prompts

### Stage 4: AI Strategist
- AI as powerful partner for complex tasks and large-scale refactoring
- Multi-agent workflows with planning and coding models
- Focus shifts to **delegation** and **verification**
- Confident and optimistic about the future

## The New Developer Role (Stage 4)

> "They now focus on the delegation and the verification of a task."

- **Delegation**: Rich context, instructions, reviewing AI plans, tweaking before proceeding
- **Verification**: Tearing down the agent's work — reviewing that implementation meets objectives and conventions

## Key Finding

50% of Stage 4 developers believe 90% AI-written code is realistic within 2 years; the other 50% say within 5 years. Neither group feels their value is diminished — their role is **reinvented**, not eliminated.

## Skill Priorities at Stage 4

1. **AI fluency**: Understanding capabilities and constraints of different models
2. **Delegation & agent orchestration**: Context engineering, task decomposition, parallelization
3. **Human-AI collaboration**: Tight feedback loops, stopping points, self-critique prompts
4. **Fundamentals**: Code comprehension, algorithms, systems — required for verification
5. **Verification & quality control**: Rigorous review of AI-generated code
6. **Product understanding**: Systems thinking, user needs, outcome orientation
7. **Architecture & systems design**: Elevated importance as AI handles implementation

## Contradictions with Other Sources

- [[summaries/thoughts-on-slowing-down--summary]] argues that the Stage 4 "AI Strategist" approach often leads to compounding booboos and unmaintainable codebases — a more cautionary perspective on agent delegation

## See Also

- [[concepts/agentic-coding-risks]]
- [[entities/Thomas-Dohmke]]
- [[topics/ai-software-development]]

## Sources

- [[summaries/developers-reinvented--summary]]
