---
title: "The engineer’s guide to building a software factory"
source: "https://leaddev.com/software-quality/the-engineers-guide-to-building-a-software-factory"
author:
  - "[[Chris Kelly]]"
published: 2026-09-10
created: 2026-10-01
description: "Coding agents alone plateau at 20 to 30% gains. Real progress comes from building a software factory of multi-agent loops."
tags:
  - "clippings"
---
You have **1** article left to read this month before you need to [register](https://leaddev.com/register) a free LeadDev.com account.

**Key takeaways:**

- Individual agents plateau at **20-30% gains**, not the **2-3x** teams expect.
- The fix is to use **multi-agent loops** with separated objectives, not one agent checklisting.
- Three loops lead: **PR→merge**, **Ticket→PR**, **Alert→resolution**, each with major measured gains.

---

In conversations with hundreds of [engineering leaders](https://leaddev.com/the-engineering-leadership-report-2026/), I keep hearing the same pattern. Teams went in expecting [coding agents](https://leaddev.com/ai/best-ai-coding-assistants) to make them 2-3x more productive. What they actually see at the org level is more like 20-30%, which is real, but not what anyone was promised.

The reason is that individual adoption changes one engineer’s workflow, not the team’s delivery system. [Code gets written faster](https://leaddev.com/ai/as-ai-helps-us-write-more-code-whos-catching-the-bugs), but it still moves through the same review queues, the same planning cycles, the same deployment process.

I’ve been calling this the productivity plateau, and step-function gains only come when everything around the code speeds up too.

## Your inbox, upgraded.

Receive weekly engineering insights to level up your leadership approach.

## The vision: a software factory

Speeding up everything around the code means a system that works at the level of the team, one that coordinates humans, agents, context, tools, verification, and feedback across the whole delivery process.

Individual coding [agents](https://leaddev.com/technical-direction/how-to-prepare-for-ai-agents) can’t supply that, however good they get. Each one starts from zero and stops at the edge of its own task. It has no memory of the last run and no interest in what happens after it hands off.

I call that system a software factory. I know the word makes some engineers flinch, so let me be clear about what I mean. A factory isn’t about volume, and it’s definitely not about slop. It’s instrumented, repeatable, quality-gated production: throughput measured in outcomes, issues caught by the process, and skilled people spending their time on the highest-leverage judgment calls.

Nobody builds one in one go. You build it one production line at a time.

## Production lines are agentic loops

Each production line is an agentic loop. It takes a recurring job in the software development lifecycle and handles it end to end. A [bug report](https://leaddev.com/software-quality/keep-calm-code-face-bugs) comes in and a merged fix goes out. A vulnerability gets flagged and it closes. Agents do the repetitive work in the middle, humans step in at the moments that actually need them, and every run leaves the loop better set up for the next one.

The thing people get wrong about loops is picturing one agent working through a checklist. In practice it’s several [agents](https://leaddev.com/technical-direction/why-everyones-suddenly-talking-about-ai-agents), each with its own objective, tools, and acceptance criteria. One assesses the risk of a change. One does the work. One tries to find fault with it. One decides whether a human needs to see it.

That separation is what makes the output trustworthy. An agent grading its own work will pass its own work, every time. Give each agent a different objective and every stage has something checking it that wants a different result. It’s the same reason you don’t let engineers approve their own PRs.

Connect enough of these loops and you stop managing agents one at a time.

## Three loops to start with

Across the engineering organizations we work with, the same three loops keep showing up first. The order varies, but the pattern is remarkably consistent, and the reason is usually the same: teams pick whatever hurts most, build a loop around it, and what they learn reshapes how they scope the next one.

### 1\. PR → merge

This is the loop most teams need first. When agents write more code, PR volume rises and the constraint becomes confidence. We hit that wall ourselves with 1,400+ PRs open and median time to first human comment around 20 hours.

The loop starts when a PR opens and ends at a verified merge. A risk analyzer routes the change, auto-approving low-risk PRs and tagging higher-risk ones for human input. A deep reviewer checks correctness line by line: is there an objective bug? A PR fixer repairs findings, CI failures, and merge conflicts, so most issues resolve without another human round-trip. A verifier deploys to an isolated instance, exercises the affected behavior, and posts inspectable proof – logs, screenshots, a replayable trace. An intent reviewer asks whether the change makes sense in the broader system and surfaces the decisions that need human judgment. A memory manager distills the feedback into per-repo knowledge every agent reads next run.