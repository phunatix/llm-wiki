---
title: Dark Side of Self-Service  | Humanitec
source: https://humanitec.com/blog/what-developer-self-service-shouldnt-look-like
author:
  - "[[Kaspar von Grünberg]]"
published:
created: 2026-02-18
description: Developer self-service is a fundamental step every engineering team needs to take to reach true DevOps, true “you build it, you run it”. Often however, teams get self-service spectacularly wrong. This article will walk through some real-life examples and discuss how you should think about striking the right balance between golden cages and golden paths.
tags:
  - clippings
  - sre
  - devops
  - self-service
  - developer-experience
---
## Dark Side of Self-Service

August 27, 2021

Developer self-service is a fundamental step every engineering team needs to take to reach true DevOps, true “you build it, you run it”. Often however, teams get self-service spectacularly wrong. This article will walk through some real-life examples and discuss how you should think about striking the right balance between golden cages and golden paths.

![](https://cdn.prod.website-files.com/64462c9aa967772377e53b6e/64462c9aa96777ca6ce54236_6128ce1409e2fc143cab75cb_Frame%2520201.webp)

⚠️ This post covers Platform Orchestrator v1. v2 is now available with simplified architecture and support for any compute target. See differences between the two products [here](https://developer.humanitec.com/platform-orchestrator/docs/what-is-the-platform-orchestrator/orchestrator-v1-and-v2/)

Developer self-service is the best thing that can happen to a team. “You build it, you run it” is what you would want for your engineering team. It’s setting the right incentives, unblocking developers, reducing [cognitive load](https://platformengineering.org/blog/cognitive-load). Developer self-service means striking the right balance between overwhelming people by letting them operate everything and restricting them by building abstractions. In fact, developer self-service is often used as an excuse for either shifting work left or for belittling developers. In this article, I want to explain how not to approach developer self-service, which might be even more important than learning how to enable it in the first place.

## Shooting yourself in the foot

We’re all bought in on the paradigm “you build it, you run it”, right? I mean this is literally what DevOps is all about. Heroically tearing down walls between “operations” and “application development”. We’re all one now, everybody does everything!

“Developer self-service” is just a modern reincarnation of that motto. It’s more 2021, it’s confirmed as important by enough people with enough followers on Twitter and it leaves enough room to interpret it the way you want.

In my opinion, it actually leaves room to be **abused** the way certain people want. Because both, the “you build it, you run it'' paradigm and the newer “developer self-service”, are being abused by certain roles in the engineering team to avoid doing their job properly and instead waste time on “nice to have” stuff. While the early 2000s were dominated by application developers throwing unstructured code “over the fence” to operations and sysadmins to somehow get it to run, we’re now experiencing the opposite: operations teams (or wrongly named DevOps teams) that come up with yet another cool technology and throw it at the application development team so they can “self-serve” it, without proper training. Many also enjoy building abstractions that [restrict the freedom](https://humanitec.com/blog/devops-standards-vs-freedom) of the individual developer. If your abstractions work in 90% of cases but the remaining 10% are a pain, you don’t win much.

This is why it is insanely important to get the balance between the two right. It’s important for the sanity of developers and equally important for managing the workload of the operations team building (or not building) abstractions.

If Ops don’t do their job properly, all they are doing is creating more work for themselves and everyone else. Because who do developers slack if they don’t know how to debug those nasty Helm charts? Correct, operations. Which in turn can go back and complain that they are missing their quarterly targets. It’s a vicious cycle.

![](https://cdn.prod.website-files.com/64462c9aa967772377e53b6e/64462c9aa967773810e5415a_6128cc90e4a54c0f49c940c4_w-Cchwbo0EujVKE2PWRKoWglZ75FmOvWklTrC4qYM7UVZuUMoXnvau3-4YRE7aLK-Rjet4S-UCxse7sZ-JaNtZ4hvTzeI-XIhswC4vT1XQXyNBCioLWQnkfswcsXqvc2KsUrmQRF%253Ds0.png)

You can clearly see this in the data. When we analyzed the setups of 1,856 engineering teams across the world, we asked what sentence would describe their DevOps setup best. Full “you build it, you run it” is by far not the majority, coming in at 21.2%. 32.2% are running an old-school throw-over-the-fence setup. Interesting is the remaining 44.6%. Those are the teams that basically tear down the walls, while at the same time overwhelming the majority of their developers with delivery tasks they aren’t prepared for. Who fills in are senior developers that take over the “de facto” role of old-school operations. There is little evidence this situation is better than the standard split between a sysadmin and a developer.

## There’s nothing wrong with division of labour

![](https://cdn.prod.website-files.com/64462c9aa967772377e53b6e/64462c9aa96777f71ae54159_6128cc8f403155ee55c58269_wA_xlthAm5xi85wOXSlCB1K-0Q4bJ8d6N_jUCbcLBVtrYGTeBtjR2aaEpLJ1R72RYupy6eRLlvltSE60wK_AfTxy-btVxQgrp0qMC_AwAx045lLo3zgfSmaeS3xrV5S3JJkNocwb%253Ds0.png)

The first thing to do here is to acknowledge that there is always some sort of division of labor. At enterprise-scale, a no-ops world is a nice dream, but not much more than that.

To quote my friend Aaron Erickson, who built Salesforce’s Internal Developer Platform:

*“Service ownership is a good idea in theory, but in practice people get confused. If developers have to run all the ops for their services, you do not have any economies of scale. To run 1,000 different services around Kubernetes, you shouldn't need 1,000 Kubernetes experts to do that.”*

The question in reality is not about erasing the role of operations, it’s about defining what the right hand-over point between Ops and developer is. Rather than running an operations team, the way to go is running an [internal platform team](https://humanitec.com/blog/internal-platform-teams-what-are-they-and-do-you-need-one) that focuses on lowering cognitive load through self-service. I will explain this using the “cognitive load” theory at the end of this article.

## Some truly bad examples

Enough of the high-level. Let me give you two examples of setups that sound beautiful at first glance, but actually got the self-service balance totally wrong. They both highlight the arrogance of this new “leave developers alone” philosophy.

### The “throw everything at them” crew

This example stems from a conversation I’ve recently had with an SRE at a fast scaling startup. Let’s have a look at the setup this team built and what’s wrong with it.

The company was operating with customers from one continent, with no particular data-protection requirements. They were running 4 apps in production. Each application consisted of roughly 20 microservices, mostly written in Python for the backend and ReactJS for the frontend. The company offered a B2B SaaS product, loads were almost 100% predictable, scalability wasn’t a problem at all. They were able to set things up with no legacy (a luxury that no enterprise vendor usually has), from scratch.

Let’s say we strictly optimize for developer self-service (and experience), what’s the **only** thing this team should be using? The answer is a cheap advertisement for Heroku (not associated with them and the link doesn’t contain any kickback). Even this smart SRE couldn’t give me a single reason why not to choose this. But Heroku is boring. It doesn’t look smart, it doesn’t make you feel like a wizard or witch, it’s not open source and it’s not recommended by the CNCF. In other words: if you’re cool, you don’t use Heroku.

So the team went off and built the following beautiful setup: Kubernetes with EKS and a local provider (because somebody in the business said this would drive sales in one geography). This local provider didn’t offer managed K8s so they used a self-managed version. Four different DB types, some of them managed. Elastic, Redis, RabbitMQ. CI with Jenkins and GitHub Actions (why would one standardize). Argo to sync the mess with the cluster.

Then Terraform, of course, let’s IaC everything, pour Snyk on top and throw it over the fence.

Those things were all somewhat connected through scripts, no abstraction, everybody does everything. If somebody asks, respond with “you build it, you run it”. Next, you might want to write a fancy article on Medium to describe your setup. Make sure you use the words “GitOps”, “Continuous Deployment” and finish with a lot of super complex flow diagrams.

![](https://humanitec.com/blog/)

I asked the SRE straight up: “Do you think your developers feel comfortable operating your system?” To which he responded, “I cannot imagine they do”. “Have you asked them”? “No, that’s the way we want it”.

So to summarize: rather than teaching teams one tool that is easy to maintain and operate, developers now have to operate: Terraform, Helm Charts, Argo, Jenkins, Grafana, Snyk. And that’s just scratching the surface. What was actually won? Nothing. And it’s not that developers are dumb, of course. They could learn how to do all of this. Helm Charts aren’t rocket science. But what was won?

### The “take it all from the” crew

My other example comes from a really large company that builds lots of stuff around cars and has thousands of developers. If you ask any developer about their central platform unit, they get angry (if you’re lucky).

This unit has come to the conclusion that developers actually don’t need that much choice and that they could make most decisions centrally for them. They’ve not only abstracted everything away from them, they’ve literally taken any room to respond to the specific needs of individual teams. Developers don’t understand what goes on inside the black-box platform that was built and are totally dependent on the central platform team to increase functionality.

In this case, there is literally no way to circumvent the default. Developers don’t know what’s happening under the hood, they have no idea how things turn out, they simply don’t trust the system. This only exacerbates the fact that in reality in application development it is already hard to forecast what default the team will require. To believe that a platform team can cover 100% of cases is naive. What happens is that developers first wait for new functionality, the platform team doesn’t deliver, then they simply revolt and abandon the platform altogether. You again win nothing.

![](https://cdn.prod.website-files.com/64462c9aa967772377e53b6e/64462c9aa96777339ce54155_6128cc8f9a4a2a26c0350b5f_STRZ4YJ92EcvOjFUF7p8QeCeKLKBSMkn0ptPac_ynKUu9UNVgj76m9siCGp3P3r0tWRe7xQe82Cop8yRF9jxFaVgPg8OgZiOC7nj04X-kLF579QIL2k_WgIoRRBUIQB1VYzNz0xW%253Ds0.jpeg)

## The “cognitive load” tradeoff

The two examples above are extremely negative and present both extremes. But how do you think about this the right way? How do you determine how much to throw at your team vs how much you abstract away? I’ve developed a model to help you structure your thoughts around this and I call it the “cognitive load” trade-off. Because this is exactly what it comes down to: cognitive load.

Let me explain. It’s probably fair to assume that developers are somewhere on the right of the bell curve of IQ distribution. In plain words: they are smart and of course, they are able to figure out how to run Terraform at scale if they have to. But while they’re becoming IaC wizards, they fall back on their area of specialization. It’s not what their managers (and the market) pays them for.

The decision that we have to take is how much cognitive load we want to throw at them. More complexity, more cognitive load. The only way to determine this is through good old communication. That’s the single most important component here. How deep do they want to go? What do they feel comfortable with? How much time can we allocate for learning new stuff?

We can think about this theoretical too. Simply map cognitive load against the complexity of the setup. The more complex your setup, the higher the cognitive load.

If we would need to map our examples above, the Heroku setup would be on the left. The setup the SRE geniuses of the first example came up with is on the right side. Huge amount of cognitive load, huge amount of complexity for the developers to handle.

![](https://cdn.prod.website-files.com/64462c9aa967772377e53b6e/64462c9aa96777733be54157_6128cc9081bd9b35923f2c22_kYKychy3aXEYgMCwXvmmd54W6tE7pPgcGVvCe7VQQGn-rgCAC7jhMCggMPDxeaneBS2ywbgcjDIUSLHXw2705UigNTfaCBhG0bT8sS8MUuyDFLfkiNZZTrSDTFdJFeZWADAT1p3x%253Ds0.png)

How much cognitive load somebody is willing to handle varies from team to team. Well-run engineering teams communicate enough to understand the team’s (or even the individual's) preference for cognitive load. Beyond this load, they build opaque abstractions (golden paths) that help developers understand what’s going on under the hood while limiting further cognitive load.

![](https://cdn.prod.website-files.com/64462c9aa967772377e53b6e/64462c9aa967774118e54158_6128cc900250316d28ede39c_kSLTtRbIeuf__tKADLiA8kpEEJUrocttk0G-az0xTX0ENqjvabgWBz9MDbxUhFZnMjy9kGQ3OqJ4TwsrdeyQkVExgr7wSNCpGmAQIfXjbBwC4W_Vbozp4EmAx3Yp_RNyo0C2NJ-K%253Ds0.png)

## Golden paths, not cages

Let’s assume we’ve figured out the amount of cognitive load our developers can handle while doing everything we expect from them. That means the rest has to be abstracted or handled for them.

In our second example, we’ve seen the disastrous effects of high levels of abstraction. The key here is to go for golden paths over golden cages and to constantly (constantly!) keep communicating, I really cannot stress this enough. A golden path is about abstracting without abstracting. Developers understand what’s under the hood, they could go low-level, you don’t keep them from doing this. All you do is give a guarantee that things are easier if you stick to the paths. What we see in the data is that 97% of developers stick to a golden path once established, following the “social contract” that staying on the path makes the setup more scalable and easier to operate for everybody.

Jason Warner, CTO at GitHub, explained this well when he detailed out how they introduced their self-service setup, freed people from pager duty, and made them go fast without restricting anybody from going low-level.

[3 How was the Internal Developer Platform designed and built?](https://youtu.be/ZRVrNak9RoM)

Github engineers are arguably among the best in the world. [To quote Jason further](https://humanitec.com/blog/jason-warner-why-github-built-their-own-internal-developer-platform):

*“We understand these concepts better than anybody on the planet. In the end we invented 90% of all concepts we use today”.*

That’s self-confident but true. Not even at Github developers interpret “you build it, you run it” as developers doing everything. If they don’t do it that way, you shouldn’t either.

And just to reiterate on this one: if you communicate you win. You have to treat developers as users, you have to iterate with them, you have to explain why the golden path makes sense and why they should use it for the good of everybody.

And to end with some shameful self-advertisement but one I deeply believe: [Internal Developer Platforms](https://humanitec.com/blog/what-is-an-internal-developer-platform) can help you build self-service setups that make for wonderful golden paths. They help you “abstract” without keeping things away, they let you expose just the right amount of cognitive load for every single developer.

![](https://cdn.prod.website-files.com/64462c9aa967772377e53b6e/6450b26051a4501f1af34ebc_Kaspar%20von%20Gru%CC%88nberg.webp)

CEO at Humanitec

[

LinkedIn

](https://www.linkedin.com/in/kaspar-von-gr%C3%BCnberg-73872380/)

Kaspar is an early pioneer in platform engineering. Over the last decade he has been building Internal Developer Platforms (IDPs) at scale, and is responsible for coining the term IDP. A regular speaker on the topic of platform engineering, Kaspar is the author of several associated defining articles. He is also the founder and CEO of Humanitec, the company behind Score and the Platform Orchestrator which is now the centerpiece at the majority of dynamic IDPs.

## Upcoming events

Community

[Events](https://humanitec.com/events)