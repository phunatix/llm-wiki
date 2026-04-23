---
title: "Summary: Building a Golden Path to AI (InfoWorld)"
type: summary
source_count: 1
created: 2026-04-23
last_updated: 2026-04-23
tags:
  - summary
  - golden-path
  - ai-adoption
  - platform-engineering
  - developer-experience
source_file: "raw/inbox/Building a golden path to AI.md"
related_pages:
  - concepts/golden-paths
  - topics/platform-engineering
  - topics/ai-software-development
  - concepts/europe-ai-dependency
status: complete
---

# Summary: Building a Golden Path to AI

**Source**: InfoWorld — "Building a golden path to AI"
**Author**: Matt Asay
**URL**: https://www.infoworld.com/article/4079018/building-a-golden-path-to-ai.html
**Published**: 2025-10-26 | **Clipped**: 2026-04-23
**Type**: Opinion / architectural recommendation

---

## What This Source Contains

Matt Asay applies the golden paths + guardrails-over-gates framework (explicitly citing Bryan Ross) to the specific challenge of enterprise AI adoption. Argues that the same mistake of building a monolithic official platform — previously made with cloud and SaaS — is being repeated with AI, and proposes a composable API + guardrails approach instead.

---

## Key Takeaways

### The AI Velocity Gap
Developers are already using AI faster than leadership can standardize it. Recent surveys confirm: developers adopt AI faster than project leaders can establish policy. This gap — not developer speed — is the real risk. The result is shadow AI: developers using personal credit cards to access APIs, creating unmonitored, unsecured data flows inside the enterprise.

### Why the Official Platform Approach Fails for AI
Building the "one true enterprise AI platform" over 18 months is worse for AI than for earlier technology waves:
- The model selected will be surpassed 5× before adoption
- Different models excel at different tasks (legal summarization ≠ Python refactoring ≠ K8s manifests)
- Centralized prediction is structurally incompatible with a moving target

### Composable AI Guardrails

**Layer 1 — Interface standard**: OpenAI-compatible API as de facto contract, fronted by an API gateway. Backend-agnostic — teams can swap models without rewriting their stack. Enables model competition without fragmentation.

**Layer 2 — Structured outputs**: Enforce JSON-constrained outputs via schema at the gateway. The difference between a demo and a production system.

**Layer 3 — Observability**: OpenTelemetry genAI semantic conventions. Track prompts, model IDs, tokens, latency, and cost in existing SRE tooling. Visibility enables effective cost guardrails.

**Layer 4 — Data governance**: Runtime secret retrieval (no embedded keys). Unified authorization to enterprise IAM. Minimize new attack surfaces.

**Layer 5 — Exception handling**: Proceed-with-justification flag for off-path AI use. Extra logging + security review + tighter budgets. Log and review weekly.

### The Cognitive Load Argument
> "The cognitive load of model selection, prompt hygiene, retrieval patterns, and cost management is high; the platform team's job is to lower it."

This is the same framing as golden paths generally — the platform exists to reduce undifferentiated complexity so developers can focus on the actual problem. AI just raises the cognitive load bar higher than previous technology generations.

---

## Connections to Existing Wiki

- **[[concepts/golden-paths]]** — extends the guardrails-over-gates framework to AI; the AI-specific section of the concept page draws from this source
- **[[topics/platform-engineering]]** — AI is now a first-class challenge for platform teams, not just a feature request
- **[[topics/ai-software-development]]** — complementary angle: while that topic covers how AI changes developer workflows, this covers how platforms should govern AI use
- **[[concepts/europe-ai-dependency]]** — the "shadow AI" phenomenon is a manifestation of the velocity gap this article describes
