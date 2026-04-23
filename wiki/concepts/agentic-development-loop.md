---
title: Agentic Development Loop
type: concept
source_count: 1
created: 2026-04-23
last_updated: 2026-04-23
tags:
  - concept
  - ai-agents
  - developer-productivity
  - claude-code
related_pages:
  - concepts/agentic-coding-risks
  - concepts/ai-developer-stages
  - concepts/forward-deployed-engineer
  - topics/ai-software-development
status: complete
---

# Agentic Development Loop

## The Core Insight

From Neil Kakkar's practitioner account of six weeks working with Claude Code at Tano:

> "I'm not the implementer anymore. I'm the manager of agents doing the implementation. And managers automate their team's grunt work."

The shift isn't just using AI to write code faster — it's a **role identity change**. The developer becomes the orchestrator of agents: setting direction, reviewing output, building infrastructure that makes agents more effective. This frames the productivity gain not as a feature of the AI tool, but as a consequence of adopting a new working model.

---

## The Friction-Removal Loop

Kakkar documents four sequential friction-removal steps, each revealing the next:

| Step | Friction Removed | Mechanism |
|---|---|---|
| 1. `/git-pr` skill | **Formatting** — writing PR descriptions | Claude Code skill automates staging, commit messages, PR creation |
| 2. SWC bundler | **Waiting** — 60-second builds break flow | Sub-second rebuilds eliminate the attention-drift gap |
| 3. Agent UI preview | **Verification** — human checks every UI change | Agent verifies its own output; human only reviews final result |
| 4. Worktree + port system | **Context-switching** — parallel branches collide | Each worktree gets unique port range; 5 agents run simultaneously |

The sequence follows the **Theory of Constraints**: fix the biggest bottleneck, and the next bottleneck immediately becomes visible. Removing PR friction exposed build wait time. Removing build wait time exposed the inability to parallelize. Removing parallelization friction exposed verification overhead.

---

## Key Mechanisms

### The `/git-pr` Skill
A Claude Code skill (slash command) that reads the full diff and writes a more thorough PR description than a human would write mid-flow. Key insight: the "context switch" from coding mode to describing-code mode is itself a hidden cost. Eliminating it compounds across every PR.

### Sub-Second Build Feedback
Switching from a slow bundler to SWC (Rust-based) dropped build times from ~60 seconds to <1 second. The threshold isn't incremental — it's categorical. At 60 seconds, the developer's attention leaks. At <1 second, there's no gap for attention to escape. The feedback loop becomes effectively continuous.

### Agent Self-Verification
Wiring the Claude Code preview into the agent's definition of "done" — a change isn't complete until the agent has checked the UI itself. This delegates the verification step entirely, letting agents run longer without human oversight and catch their own mistakes before they surface.

### Parallel Worktrees with Port Isolation
Environment variables sharing the same port numbers prevented simultaneous builds. The solution: each worktree gets ports assigned from a unique range at creation time. Five concurrent worktrees, each with an independent frontend and backend server, no collisions. The developer's role becomes: plan → dispatch agents → review/merge — no per-feature context-switching.

---

## The Meta-Pattern

> "Each of these stages removed a different kind of friction... And each time I removed one, the next became visible."

This is the **Theory of Constraints applied to development workflow**:
1. Identify the binding constraint (biggest source of friction)
2. Exploit it (find the immediate fix)
3. Subordinate everything else to that fix
4. Elevate (build infrastructure so the fix is automatic)
5. Repeat — the next constraint is now visible

The practical result: the developer's highest-leverage work shifts from *writing features* to *building agent infrastructure*. Friction removal is the feature.

> "The highest-leverage work I've done at Tano hasn't been writing features. It's been building the infrastructure that turned a trickle of commits into a flood."

---

## Relation to Other Wiki Concepts

**Compared to [[concepts/ai-developer-stages]]** (Dohmke's four stages):
- Kakkar's account illustrates what "Collaborator" and "Strategist" stages look like in practice — not theory, but lived workflow with specific tooling decisions

**Compared to [[concepts/agentic-coding-risks]]** (Zechner's caution):
- Kakkar represents the productive counterpart: the risks Zechner warns about (compounding errors, low recall) are mitigated here through agent self-verification and human-in-the-loop review at merge time
- Both are credible — Kakkar's system works *because* he kept humans in the review loop

**Compared to [[concepts/forward-deployed-engineer]]**:
- The FDE embeds in user teams to understand context; Kakkar's role shift is the internal equivalent — the developer embeds themselves in the agent workflow as coordinator, not implementer

---

## Quotable

> "Building things is a different kind of fun now — it's so fast that the game becomes improving the speed. When the loop is tight enough, engineering becomes the entertainment."

> "It's the infrastructure, not the AI. These aren't glamorous problems. They're plumbing. But plumbing determines whether you're in flow or wrestling your environment."

---

*Source: Neil Kakkar, "How I'm Productive with Claude Code" (2026-03-16)*
