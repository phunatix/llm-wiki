---
title: "Building a golden path to AI"
source: "https://www.infoworld.com/article/4079018/building-a-golden-path-to-ai.html"
author:
  - "[[Matt Asay]]"
published: 2025-10-26
created: 2026-04-23
description: "Developers aren’t waiting while leadership dithers over a standardized, official AI platform. Better to treat a platform as a set of services or composable APIs to guide developer innovation."
tags:
  - "clippings"
---
opinion

Oct 27, 20256 mins

## Developers aren’t waiting while leadership dithers over a standardized, official AI platform. Better to treat a platform as a set of services or composable APIs to guide developer innovation.

![Light trail flash, neon yellow and orange golden glow path trace effect](https://www.infoworld.com/wp-content/uploads/2025/10/4079018-0-97957700-1761555707-istock-1214773708-100936887-orig.jpg?quality=50&strip=all)

It’s clear your company needs to accelerate its AI adoption. What’s less clear is how to do that without it being a free-for-all. After all, your best employees aren’t waiting on you to establish standards; they’re already actively using AI. Yes, your developers are feeding code into [ChatGPT](https://www.infoworld.com/article/2338069/chatgpt-and-software-development.html) regardless of any policy you may be planning. Recent surveys [suggest developers are adopting AI faster than their leaders can standardize it](https://devops.com/survey-sees-developers-embracing-ai-faster-than-project-leaders/); that gap, not developer speed, is the real risk.

This creates what [Phil Fersht calls an “AI velocity gap”](https://www.horsesforsources.com/stop-guessing-your-ai-velocity-gap-start-measuring-it-before-mkt-measures-you_102125/): the chasm between teams frantically adopting AI to win and central leadership dithering over the risk of getting started. Sound familiar? It’s “shadow IT” all over again, but this time it’s powered by your data.

[I’ve written about the hidden costs of tech sprawl](https://www.infoworld.com/article/2334740/unfettered-developer-freedom-may-be-over.html), whether it was unfettered developer freedom leading to unmanageable infrastructure or the [lure of multicloud](https://www.infoworld.com/article/2334455/one-significant-cost-of-multicloud.html) turning into a morass of interoperability nightmares and cost overruns. When every developer and every team picks their own cloud, their own [database](https://www.infoworld.com/article/2264322/how-to-choose-the-right-database-for-your-application.html), or their own [SaaS](https://www.infoworld.com/article/2256637/what-is-saas-software-as-a-service-defined.html) tool, you don’t get innovation—you get chaos.

This may be the status quo, but it’s a recipe for failure. What’s the alternative?

## The problem with official platforms

The temptation for a platform team is to see this chaos and react by building a gate. “Stop! No one moves forward until we have built the official enterprise AI platform.” They’ll then spend 18 months evaluating vendors, standardizing on a single [large language model](https://www.infoworld.com/article/2335213/large-language-models-the-foundations-of-generative-ai.html) (LLM), and building a monolithic, prescribed workflow.

Good luck with that.

By the time they launch that one true platform to rule them all, it will be hopelessly obsolete. Heck, at the current pace of AI, it risks obsolescence before adoption. The model they standardized on will have been surpassed five times over by newer, cheaper, and more powerful alternatives. Their developers, long since frustrated, will have routed around the platform entirely, using their personal credit cards to access the latest APIs, creating a massive, unsecured, unmonitored blind spot right in the heart of the business.

Trying to build a single, monolithic gate for AI won’t work. The landscape is moving too fast. The needs are too diverse. The model that excels at summarizing legal documents is terrible at writing [Python](https://www.infoworld.com/article/2253770/what-is-python-powerful-intuitive-programming.html). The model that’s great for marketing copy can’t be trusted with financial projections. Even within engineering, the model that’s brilliant at refactoring [Java](https://www.infoworld.com/article/2335696/11-reasons-the-new-java-is-not-like-the-old-java.html%20https://www.infoworld.com/article/2335996/7-reasons-java-is-still-great.html) is useless for writing K8s manifests.

The problem, however, isn’t the *desire* for a platform; it’s the *definition* of one.

## From prescribed platforms to composable products

[Bryan Ross recently wrote a great post on “golden paths”](https://newsletter.bryanross.me/p/golden-paths-one-size-does-not-fit) that perfectly captures this dilemma. (It builds on other, earlier arguments for these so-called golden paths, like [this one on the Platform Engineering blog](https://platformengineering.org/blog/how-to-pave-golden-paths-that-actually-go-somewhere).) He argues that we need to shift our thinking from “gates” to “guardrails.” The problem, as he sees it, is that platform teams often miss the mark on what developers actually *need*.

As Ross writes: “Most platform teams think in terms of ‘the platform’—a single, cohesive offering that teams either use or don’t. Developers think in terms of capabilities they need right now for the problem they’re solving.” So how do you balance those competing interests? His suggestion: “Platform-as-product thinking means offering composable building blocks. The key to modular adoption is treating your platform like a product with APIs, not a prescribed workflow.”

Ross nails the problem. Now what do we do about it?

Instead of asking a committee to pick *the* model, platform teams should instead build a set of services or composable [APIs](https://www.infoworld.com/article/2269032/what-is-an-api-application-programming-interfaces-explained.html) that channel developer velocity. In practice, this all starts with a de facto interface standard. One de facto standard is the OpenAI-style API, now supported by multiple back ends (e.g., [vLLM](https://docs.vllm.ai/en/latest/serving/openai_compatible_server.html)). This doesn’t mean you bless a single provider; it means you give teams a common contract, probably fronted by an API gateway, so they can swap engines without rewriting their stack.

That gateway is also the perfect place to enforce structured outputs as a rule. “Just give me some text” is fine for a demo but won’t work in production. If you want durable integrations, standardize on [JSON](https://www.infoworld.com/article/2255837/what-is-json-a-better-format-for-data-exchange.html)\-constrained outputs enforced by schema. Most modern stacks support this, and it’s the difference between a cute demo and a production-ready system.

This same gateway becomes your control plane for observability and cost. Don’t invent a new “AI log”; instead use something like OpenTelemetry’s emerging [genAI](https://www.infoworld.com/article/2338115/what-is-generative-ai-artificial-intelligence-that-creates.html) semantic conventions so prompts, model IDs, tokens, latency, and cost are traceable in the same tools site reliability engineers already run. This visibility is precisely what enables effective cost guardrails.

The critical bedrock of all this is data access governance. This is an area where you need to be resolute, keeping identity and secrets where they already live. Require runtime secret retrieval (no embedded keys) and unify authorization to your enterprise [identity and access management](https://www.csoonline.com/article/518296/what-is-iam-identity-and-access-management-explained.html). The goal is to minimize new attack surfaces by absorbing AI into existing, hardened patterns.

Finally, allow exits from the golden path but with obligations: extra logging, a targeted security review, and tighter budgets. As Ross recommends, build the override into the platform, such as a “proceed with justification” flag. Log these exceptions, review them weekly, and use that data to evolve the guardrails.

## Platform as product, not police

Why does this “guardrails over gates” posture work so well for AI? Because AI’s moving target makes centralized prediction a losing strategy. Committees can’t approve what they don’t yet understand, and vendors will change from under your standards document anyway. Guardrails make room to safely learn by doing. This is what smart enterprises already learned from cloud adoption: Productive constraints beat imaginary control.

As I’ve argued, carefully limiting choices enables developers to focus on innovation instead of the glue code that becomes necessary after development teams build in diverse directions. This is doubly true with AI. The cognitive load of model selection, prompt hygiene, retrieval patterns, and cost management is high; the platform team’s job is to lower it.

Golden paths let you move at the speed of your best developers while protecting the enterprise from its worst surprises. Most importantly, this approach meets your organization where it is. The individuals already experimenting with AI get a safe, fast on-ramp that doesn’t feel like a checkpoint. Platform teams get the compliance, visibility, and cost controls they need without feeling stymied by process. And leadership gets the one thing enterprises are starved for right now: a way to turn a thousand disconnected experiments into a coherent, measured, and governable program.