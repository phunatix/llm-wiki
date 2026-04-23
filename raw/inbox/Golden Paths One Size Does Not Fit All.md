---
title: "Golden Paths: One Size Does Not Fit All"
source: "https://www.chieftherapyofficer.co.uk/p/golden-paths-one-size-does-not-fit"
author:
  - "[[Bryan Ross]]"
published: 2025-11-22
created: 2026-04-23
description: "How to build a Golden Path, rather than a Golden Cage"
tags:
  - "clippings"
---
![](https://substackcdn.com/image/fetch/$s_!rMvc!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fb93abe25-5fc5-431f-a94c-fcd27d287c77_459x612.png)

There is a fundamental cultural conflict in platform engineering that’s often overlooked.

Platform teams typically approach their work from a perspective of standardisation and reliability. They’ve dealt with the fall-out from inconsistent deployments, security incidents, and audit failures. Their natural response is to reduce variability. A single, perfect, golden path for everyone to follow.

Developers, meanwhile, are optimising for something completely different. They’re focused on solving specific problems in the fastest way possible. Creative autonomy is core. And, any mandate to work in a particular way becomes the problem, separate from the technical merits of what you’ve built.

**Individual teams making rational decisions create organisational fragmentation.**

A team avoids your centralised platform because their tools are slightly better for their specific workload. When twenty teams make that same choice, you end up with fragmented tooling, inconsistent processes, and knowledge sharing completely evaporates. Each team optimises locally while organisational risk compounds.

Development teams optimise within their local context because that’s what they can see and control. Platform teams operate with organisational visibility, trying to optimise globally. This maps directly to what theorists call “local vs. global rationality”: decisions that make perfect sense at the team level create dysfunction at the system level.

The usual response is to crack down harder; mandate full adoption, close all escape hatches. But this pushes workarounds deeper underground where you have even less visibility.

The better question is: how do we make safety compatible with autonomy?

### Guardrails over Gates

The shift that I’ve seen work is distinguishing between what genuinely must be universal and what can be flexible. Guardrails are baseline standards that everyone must meet, regardless of individual requirement or implementation.

You don’t mandate that everyone must drive the same car, but you do require that all cars have functioning brakes. Platform engineering needs this same distinction. The brake isn’t optional, but the vehicle choice is.

**Guardrails define the boundary conditions, not the implementation.**

I recently worked with a large financial services firm that had spent a significant amount of time and money to build a standard process that nobody would adopt. With some help, we were able to agree on just three non-negotiables: all production deployments must pass security baseline; all services must emit standardised metrics to their observability platform; and all secrets must be retrieved from their secrets management system at runtime.

Everything else became flexible. Teams could structure their repositories however made sense. They could choose their own testing frameworks. They could define their own build steps and use their own tools. Adoption went from 17% to 86% in six months, but more importantly, the platform team’s relationship with developers shifted from adversarial to collaborative.

Every forced choice should have a clear answer to “what organisational risk does allowing flexibility here create?” and when defining a choice, we should ask ourselves “what can we do to offer maximum flexibility whilst mitigating risk?”.

### Components over Completeness

Most platform teams think in terms of “the platform” - a single, cohesive offering that teams either use or don’t. Developers think in terms of capabilities they need right now for the problem they’re solving.

**Platform-as-product thinking means offering composable building blocks.**

The key to modular adoption is treating your platform like a product with APIs, not a prescribed workflow. Your CI/CD pipeline shouldn’t be a monolithic template teams must accept wholesale. Instead, expose capabilities like security scanning, deployment automation, and secrets retrieval as services teams can integrate into their existing processes.

You can, of course, offer an example of how to integrate these together, but teams should have choice on what works best for them. A team building a new service might adopt everything. A team with a legacy application might have existing capabilities that they can more easily adapt to meet guardrail requirements.

This isn’t about letting teams skip your guardrails; those remain universal. It’s about letting them compose their developer experience from your components rather than forcing them into your prescribed workflow.

Consider security scanning. Rather than mandating a specific tool, require that all scans output results in a standard format like [SARIF](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=sarif) (Static Analysis Results Interchange Format) and that production deployments must have no high or critical level vulnerabilities. Teams can choose Snyk, Semgrep, or SonarQube based on their language and workflow, but they all feed into your centralised security dashboard. You get consistent visibility across the organisation without forcing tool standardisation where it doesn’t create value.

This approach requires verification mechanisms that don’t depend on teams using your specific implementation. Trust, but verify! Shift from process compliance to outcome verification. In the example above, standardised security scanning results can be independently checked. Similarly, you might make certain observability metrics mandatory and perform credential scanning across repositories to ensure other guardrails are being followed correctly.

### Making your platform the path of least resistance

Once you’ve established guardrails and modular capabilities, you create new opportunities in how you position your platform to developers.

Developers always have three options. They can build their own solutions from scratch, meeting every guardrail through custom implementation. This is technically possible but requires significant effort on their part. They could selectively consume platform components, using your secrets management to meet that guardrail, building their own deployment pipeline. Or they can adopt the platform fully, getting guardrail compliance baked in plus additional capabilities they didn’t have to build.

The challenge is to make that third option the obvious choice without making it mandatory.

I’ve seen this work when platform teams explicitly communicate the trade-offs. “You can absolutely build your own deployment pipeline. Here’s the security scanning integration you’ll need to implement. Here’s the audit logging format. Here’s where your metrics need to flow. Or, use our pipeline and get all of that plus automated rollbacks, deployment analytics, and integration with our incident management system.”

The message becomes: meeting guardrails is non-negotiable, but we’ve done the work to make that painless if you use our components. The more you adopt, the less undifferentiated heavy lifting you do yourself.

### Making room for reality

No matter how well you design your standards, edge cases will emerge. A critical hotfix that needs to skip the usual approval workflow. A legacy system that can’t integrate with your secrets management yet. The worst thing you can do is force developers to break out of your platform entirely when they hit these cases.

I recommend that you build the exception process directly into your platform. One team I worked with implemented a simple exception system in their CI pipelines whereby developers could set an “ *override\_security\_scan* ” flag with a required justification field. The deployment proceeded, but it triggered a notification to the security team and got logged for weekly review. Most overrides turned out to be legitimate edge cases, and the pattern analysis helped the platform team identify where their guardrails needed adjustment.

## Building platforms that flex

The framework to building platforms that developers choose to use is straightforward:

- Establish universal guardrails based on genuine organisational risk, not convenience.
- Build modular capabilities that teams can consume independently rather than forcing wholesale adoption.
- Make your platform the path of least resistance by absorbing the complexity of compliance, not by eliminating choice.
- Design exception handling directly into your system so edge cases don’t force teams to abandon you entirely.

Crucially, this approach requires a different relationship with your developer community. Instead of positioning yourself as the gatekeeper of “the right way,” you become the team that makes hard things easy. You’re not eliminating their autonomy; you’re reducing their toil. The platform becomes valuable because it solves real problems, not because leadership mandated its use.

I’ve watched this transformation happen at organisations ranging from 20 to 20,000 engineers. The mechanics vary, but the fundamental shift remains the same: from standardisation through control, to standardisation through attraction.

Like any product, the real measure of a successful platform isn’t adoption, but whether developers would choose your platform even if they weren’t required to.

One size does not fit all, but well-designed guardrails fit everyone.

---

If you enjoyed this article, you might also want to check out the submissions from other CNCF Content Club members, including:

- Steve’s piece about why [making platforms optional forces platform teams to build what developers actually need instead of mandated golden cages](https://stevefenton.co.uk/blog/2025/11/avoiding-golden-cages/).

---

*Want to dive deeper into building platforms that developers actually want to use? Subscribe to The Chief Therapy Officer newsletter, where I share monthly insights from the field on turning platform engineering theory into adoption reality.*