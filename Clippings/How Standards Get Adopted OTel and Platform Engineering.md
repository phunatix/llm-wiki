---
title: "How Standards Get Adopted: OTel and Platform Engineering"
source: "https://newrelic.com/blog/observability/how-standards-get-adopted-otel-and-platform-engineering"
author:
  - "[[New Relic]]"
published: 2026-09-11
created: 2026-10-01
description: "OpenTelemetry didn't win on vendor neutrality alone — it won by changing how platform teams and developers work together. Here's how."
tags:
  - "clippings"
---
Why do engineering leads and decision makers in the tech industry keep choosing OpenTelemetry? A naive answer normally goes something like…

*"Well, it's because it's vendor neutral! It makes it easy to switch observability vendors with no code changes."*

While that's a fair point, it doesn't even scratch the surface of why OTel has truly taken over the instrumentation space. By the end of this piece, you'll see another perspective of why OpenTelemetry isn't just winning, it's [here to stay.](https://www.cncf.io/announcements/2026/05/21/cloud-native-computing-foundation-announces-opentelemetrys-graduation-solidifying-status-as-the-de-facto-observability-standard/)

## Migrations (and humans) are never easy

Let's be honest, critical changes in how a company deploys, operates and ultimately makes use of any tech tooling are hard. I say this as someone that's led several large-scale migrations first-hand, and has helped many teams in their tech adoption strategies. Undoubtedly, the vendor neutrality of OTel has made this process a heck of a lot easier in the observability space. In an ideal scenario, it requires no code changes: reconfigure your OTLP exporter to point to B instead of A and “job done”, right? Your data now lands at B, following standards supported by the whole industry for protocols and semantic conventions. Great for end users, great for data sovereignty.

However, those that have been through a migration of this kind know that changing APIs is, arguably, not the hardest part. Now, you may be thinking…

*"Ah! Of course! You still have to migrate everyone’s alerts, SLOs, dashboards, etc."*

Sure, you'll still need to migrate alerts, SLOs, and dashboards. But thanks to Configuration-as-Code tooling like Terraform (if you’re still doing “click-ops” to set up your config, good luck) and the recent leap in AI tooling, that’s no longer the primary hurdle. Nowadays, you can lift and shift an entire organisation’s observability setup between vendors in mere days, OTel or not. So, we can cross that off the list of hardest things too.

![](https://newrelic.com/sites/default/files/styles/300w/public/2026-09/otel_migration.webp?itok=qhiFK9pb) ![Humorous meme featuring a dialogue between two figures discussing AI, telemetry backend migration, and configuration prompts.](https://newrelic.com/sites/default/files/styles/900w/public/2026-09/otel_migration.jpg?itok=DldxGziW)

The truly hard part, as with most things in tech (or in life) is humans. Observability tools are socio-technical tools, after all. They affect every engineer in an organisation, in one way or another, and allow different groups of people to communicate effectively. As creatures of habit, changing workflows, runbooks, and the ways of working of hundreds or thousands of humans across your engineering teams is (and will always be) challenging. Especially for something as critical as observability, which many only get to interact with when they least want, or expect, any surprises, in the middle of an incident.

## So, where’s OTel’s value then?

If, thanks to AI, one can move between vendors in a matter of days, and the human/social part will always be hard regardless, where is the value in OpenTelemetry? In two words, [team interactions](https://teamtopologies.com/key-concepts-content/team-interaction-modeling-with-team-topologies).

If you have been following the evolution of Platform Engineering as a discipline, you'll be familiar with its most crucial role: abstracting complexity and reducing cognitive load for stream-aligned (i.e. product) teams, so that they can deliver better products, faster. It doesn't matter if it's observability, security, compute, cloud governance, or AI. Treating your [platform as a product](https://platformengineering.org/talks-library/platform-as-a-product), with well-defined contracts that allow for self-serve interaction modes between the platform and the users of the platform, has shown time and time again to improve developer productivity and increase software quality. This is why open standards like Kubernetes, MCP, or OpenTelemetry, continue to thrive.

Before OpenTelemetry, instrumentation code was tied to the underlying SDK used to process and export that data, and often to the backend that received it. This didn’t just apply to proprietary tooling; open source clients like StatsD or Prometheus had the same limitations. You were locked to certain implementation details like temporality (cumulative vs delta), export model (push vs pull), or even to the signals that you could correlate in telemetry context (e.g. only metrics, or only logs). Transforming that data into any other format, or correlating it across signals, required an external process to stitch things together.

So, if the role of your platform team is providing a contract to developers that says *"use this API to instrument your workloads, and we promise we won't bother you again if we change anything underneath"*, you had two options:

1. Build an API abstraction on top of that telemetry client, and be very careful not to leak implementation details or context data (e.g. thread-local state) shared between signals and execution units. Easier said than done.
2. Maintain complex external processes to perform transforms before exporting to your preferred backend, and often stitch some data together in ETL pipelines.

I've done both and, “0/10, would not recommend”.

OpenTelemetry solves this in a [very elegant way](https://opentelemetry.io/docs/specs/otel/library-guidelines/#opentelemetry-client-generic-design). As illustrated in the diagram below, it decouples the API (what developers use) from the SDK (what the observability platform team can provide a default for). Application code, 3rd party libraries, and instrumentation packages that automatically instrument well-known software can all use the same standard, future-proof API. The best part is, if you don't configure an SDK, the API is a no-op with zero side-effects. And, if you want to extend or even build your own SDK (although I wouldn’t advise it) you can also do it! The possibilities are endless!

As the API’s role is to provide that stable contract with developers, you can then truly tell them *"no breaking changes again, pinky promise this time"*. This creates an incredibly powerful interaction mode between developers and platform teams. The former can focus on describing their business logic using standard, future-proof APIs, and the latter can focus on wiring the SDK and pipeline complexity underneath and ensuring that engineering standards are embedded into their telemetry production. If you want to get a clear understanding of how this can be put into practice, check out this OTel Blueprint for [managed telemetry platforms](https://opentelemetry.io/docs/guidance/blueprints/managed-telemetry-platforms-for-k8s-workloads/).

This concept of abstracting complexity away with platform contracts can, and should, extend OpenTelemetry. The example below shows how a platform team can split ownership between what is provided "as-a-service" (e.g. SDK config, Collector pipelines, Terraform modules for SLOs, alerts, etc.) and what developers self-serve.

![](https://newrelic.com/sites/default/files/styles/300w/public/2026-09/Platform%20and%20New%20Relic.webp?itok=RfXicFBq) ![Detailed flowchart of New Relic's API integration and platform ownership, showcasing SDK](https://newrelic.com/sites/default/files/styles/900w/public/2026-09/Platform%20and%20New%20Relic.png?itok=I6w2URXn)

This is not a new concept. Those that remember the container orchestration discussions of 2016 will remember many saying that Kubernetes was "too complex" and it'd never triumph over simpler, more developer-friendly options like Docker Swarm. More than 10 years later, Kubernetes is the undisputed champion, and it did so not by focusing on the developer end-user, but by giving Platform Engineers the tools they need to abstract complexity for those developers. It created an ecosystem that empowers platform teams to drive adoption of best practices in ways that align with *their* engineering standards, not those dictated by the framework or the compute layer underneath.

This is also a key reason for OpenTelemetry’s success.

## Business Context and Baked-In Telemetry

As I mentioned earlier, this model allows a clear distinction between who is in charge of configuring how telemetry is processed, and who is in charge of describing their business logic. This has tremendous implications for the type of telemetry that can and should describe our systems. If you hear anyone say *“this agent will instrument EVERYTHING so your developers will have to do ZERO work”,* please *“press X for doubt”.*

![](https://newrelic.com/sites/default/files/styles/300w/public/2026-09/instrument_everything.webp?itok=FrOPQRs8) ![A skeptical character wearing a hat is paired with the word 'Doubt' in a humorous meme format.](https://newrelic.com/sites/default/files/styles/900w/public/2026-09/instrument_everything.jpg?itok=50XUvFbC)

The most important telemetry a system can emit is normally not the one that can be collected automatically. It's the stuff that truly describes your domain-specific logic and directly ties to your business outcomes, be it checkouts per product line, time to render the first search result, or tins of baked beans left on the shelves. No automatic, out-of-the-box instrumentation can give you that.

However, you need this information “in context” with the rest of your telemetry–the metrics, traces, and logs that your application produces to describe its general behaviour in terms of HTTP calls, database queries, or exceptions generated. When your shop does not have any tins on the shelf, you (or your AI agents) want to follow the RCA thread and find out what process failed in your supply chain and get as much context as possible around it.

This is also true for open source or third party libraries. When someone says *“this agent will instrument everything”* I bet they don't mean that new, unreleased feature in a critical library or system that you depend on. Even if the owner of that agent is very fast at delivering new instrumentation, it will never match the owner of the library producing telemetry from within the library itself in a standard, implementation neutral way.

With OpenTelemetry, both of these things are possible. The [vision of OpenTelemetry](https://opentelemetry.io/community/mission/) is not one where telemetry is produced as an afterthought. It's one where systems, components, and libraries instrument themselves in a standard, future-proof way, allowing the user of that library to decide how to aggregate, process, and export that telemetry, and to decorate it with their *own* business context.

This is how standards get adopted: by changing the interaction modes between the people who build a platform and the people who use it. OpenTelemetry didn't win by making vendor migrations easier, it won by letting platform teams make a promise to developers that was previously very hard to keep: focus on your business logic, we've got the rest. This is why OpenTelemetry won the instrumentation layer, and why it will keep winning for many years to come.

---

![Dan_Gomez_Blanco](https://newrelic.com/sites/default/files/styles/1x1_100w/public/2026-09/profile_2025_web.webp?h=7afb1587&itok=pCbUNXIY)

By [Dan Gomez Blanco, Principal Observability Architect](https://newrelic.com/blog/authors/dan-gomez-blanco)

Dan Gomez Blanco is a Principal Observability Architect at New Relic, where he guides organizations in adopting observability best practices and operational readiness, while bridging strategic initiatives between customers and product. With more than 15 years of experience in platform engineering, Dan has spent recent years concentrating on OpenTelemetry. He previously served on its Governance Committee and currently co-maintains the End-User SIG with a focus on OTel Blueprints. Additionally, he authored *Practical OpenTelemetry: Adopting Open Observability Standards Across Your Organization*. Outside of work, Dan enjoys playing any percussion instrument he can find.

The views expressed on this blog are those of the author and do not necessarily reflect the views of New Relic. Any solutions offered by the author are environment-specific and not part of the commercial solutions or support offered by New Relic. Please join us exclusively at the Explorers Hub ([support.newrelic.com](https://support.newrelic.com/)) for questions and support related to this blog post. This blog may contain links to content on third-party sites. By providing such links, New Relic does not adopt, guarantee, approve or endorse the information, views or products available on such sites.

780+ integrations to start monitoring your stack for free.