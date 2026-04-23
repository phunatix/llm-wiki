---
title: How to pave golden paths that actually go somewhere
source: https://platformengineering.org/blog/how-to-pave-golden-paths-that-actually-go-somewhere
author:
  - "[[Aeris Ransom]]"
published: 2023-12-13
created: 2026-04-23
description: Platform teams should pave golden paths that optimize processes for day 2 to day 50, not just day 1. Here are some examples.
tags:
  - clippings
---
More than ever, software engineering organizations are turning to platform engineering to enable standardization by design and true developer self-service. Platform engineers build an [internal developer platform](https://internaldeveloperplatform.org/what-is-an-internal-developer-platform/) (IDP), which is the sum of all the tech and tools bound together to pave golden paths for developers. According to Humanitec’s CEO Kaspar von Grünberg, [golden paths](https://www.youtube.com/watch?v=RD5krNEGspg) are any procedure “in the software development life cycle that a user can follow with minimal cognitive load and that drives standardization.” Golden paths have long been discussed as an important goal of successful platform (and DevOps) setups. 

Grünberg’s PlatformCon 2023 talk, “[Build golden paths for day 50, not day 1!](https://www.youtube.com/watch?v=RD5krNEGspg)”, dove into how and why software engineering organizations should shift their focus to golden paths for the long term, complete with specific examples. Let’s explore the problem with the way most platform teams approach golden paths, how platform teams can fix their priorities and what scalable golden paths actually look like.

## The Problem with Most Golden Paths? Bad Priorities

When deciding which golden paths to build and in what order, too many organizations make whatever comes first in the application and development life cycle their top priority. They start optimizing processes that only take place on Day 1 of the application life cycle, like how to create a new application or service via scaffolding. However, when evaluating  the entire life cycle of an application, it’s clear that golden paths for Day 1 don’t go that far. Prioritizing golden paths for day 2 to 50 (or day 1,000, for that matter) has a much larger impact on developer productivity and business performance. 

Grünberg started studying the practices of top-performing engineering organizations years before platform engineering was on everyone’s radar. He has long considered this prioritization failure one of the [top 10 fallacies in platform engineering](https://humanitec.com/blog/top-10-fallacies-in-platform-engineering), writing: “Of the time your team will invest in an application, the creation process is below 1%.” In his view, the return on investment (ROI) on this small part of the chain is too small to justify investing in its golden paths first. Organizations should instead invest in golden paths for Day 50 and beyond.

![](https://cdn.prod.website-files.com/6489e23dd070ba71d41a33b2/65706c86fc4c0ed6dd5c92f8_HX3RfnmEougLYjFbkRKUCQmokwdZWY5KLRdNN5k_dUHdC9Wf_IkJKM5Hqeir38i9PyDfESgoPgyzGD_ufVWTglWDoBUih6jKC4USyoNhn0Uf_9O9mWyaBfdxAWkiqH216z1PAHescAtD53C7PbNfc8U.avif)

## Lessons from Netflix’s platform console

The first iterations of Netflix’s federated platform console, which is a developer portal, demonstrate that not all golden paths are created equal. Senior software engineer Brian Leathem [shared](https://www.youtube.com/watch?v=36FcxlPerdQ) that one of the platform team’s  original goals was to “unify the end-to-end experience to improve usability.” Through user research, Leathem’s team found that developers were struggling with the high volume and variety of tools distributed across their workflows. They also found that limited discovery was hurting both new and tenured developers, who had difficulty onboarding or were unaware of new offerings that would improve their existing workflows.The solution they chose was a platform console, or as Leathem described it, a “common front door” for developers. 

They adopted the Backstage plugin UI so they could invest their development resources into building custom UI components for the Netflix portal. The result was a portal in which users could manage their software across the software development life cycle  in a single view. They introduced “collections,” or fleets of services for which the developer wants to view and assess performance together, to ease the burden of managing multiple services and software. They decided to use a golden path (Leathem used the term “paved road”) to tackle the discoverability problem only. To start, the golden path was a static website that featured all documentation and recommended appropriate tools for the problems developers were solving. The goal was to weave the golden paths into the console to more deeply integrate documentation with its corresponding running services. Further down the line, Leathem’s team also hoped to build functionality for developers to create, modify and operate services through the console.

In feedback on the first iteration of the platform console, Netflix developers said the “View and Access” experience was not compelling enough for them to abandon their old habits and routines. In response, the platform team  switched their focus to end-to-end workflows not available with existing tooling to keep users returning to the console. In Leathem’s PlatformCon 2023 talk, he said the approach significantly boosted the number of recurring users on the console.

Netflix’s example demonstrates that platforms need more than the developer portal component to be compelling to users. Developers want golden paths for end-to-end workflows. 

Furthermore, usability is one of many problems a platform can improve. For example, an organization can design golden paths that improve usability, productivity and scalability by focusing on end-to-end workflows. Golden paths for different workflows can enable standardization by design and true developer self-service.

## How to Prioritize Potential Golden Paths

With more of an application’s life cycle to cover, golden paths for Day 50 can be daunting to prioritize. Inspired by his research, von Grünberg proposed a simple exercise to help platform teams determine what their priorities ought to be, based on the frequency of and the waiting time for developers and operations associated with a specific procedure. The table below is an example of what this analysis could look like based on an evaluation of 100 deployments.

Hed Dek goes here.
|Procedure|Frequency (% of deployments)|Dev time in hours (including waiting and errors)|"Ops time in hours|
|---|---|---|---|
|(including waiting and errors)"|
|Add/update app configurations (such as env variables)|5%*|1*|1*|
|Add services and dependencies|1%*|16*|8*|
|Add/update resources|0.38%*|8*|24*|
|Refactor and document architecture|0.28%*|40*|8*|
|Waiting due to blocked environment|0,5%*|15*|0*|
|Spinning up environment|0,33%*|24*|24*|
|Onboarding devs, retrain and swap teams|1%*|80*|16*|
|Roll back failed deployment|1,75%|10*|20*|
|Debugging, error tracing|4.40%|10*|10*|
|Waiting for other teams|6.30%|16*|16*|

SOURCE: Sources

From this table, organizations can gain a holistic view of the processes their golden paths need to address.

Since von Grünberg shared this exercise in early 2022, he says that the explosive growth of the [platform engineering community](https://platformengineering.org/) has enabled him to observe the most common and pressing pain points across thousands of top engineering organizations and learn successful approaches to soothing them. These insights were valuable in understanding what types of Day 50 processes are the most important for platform teams to optimize and how best to optimize them. He found that tackling the most pressing pain points with golden paths first consistently netted the best ROI. More importantly, he learned that most organizations' pain points with these processes had the same root cause and could be mitigated in large part by addressing that common cause directly.

## The Universal Pain Point: Static Configuration Management 

The problem in question is that most organizations have IDPs that enable developers to deploy an updated image from one stage to another only when the infrastructure of the application does not change. These static configuration files are manually scripted against a set of static environments and infrastructure and, as a result, are prone to errors or excessive overhead when moving beyond the simplest use cases.

![](https://cdn.prod.website-files.com/6489e23dd070ba71d41a33b2/65706c87f62d012b510290e2_mDueTmo3-aI9IxU8bf1eesycglnWCA_DZ9jpyTOsCS6P1BVakUirowf1gJtcZyt79sAFrzG9tq_2qCWTJDtL4-hc8AzOCXe7iTOujiF2RPFL2OYXVK9cMCN4QqJXAeKYW2CtoT0IpwOO8G0OpIizzkY.avif)

With static configuration management, rolling back, changing configs, adding services and dependencies, and similarly complex tasks are arduous for developers. They can either choose to manage infrastructure themselves, reducing their time spent coding and creating shadow operations, or they could submit a ticket to ops, increasing their waiting times and exacerbating existing bottlenecks.

![](https://cdn.prod.website-files.com/6489e23dd070ba71d41a33b2/65706c874a27ee938e1b3416_IuUsSC76ZlB9EWKVQCaeZqp4DQt8DEVrFvrF4ale1ZGg-WgAtPp_VSIWLuSD9Do4JSiN0agAbkD-ahSdvuTasa32Twgaix9rudgrp3oJBI0RlTDG7910LBRX3Bo12hDPZ6MsrMtPMgb6Jyq833zEFCE.avif)

With static configuration management, neither developers nor ops win. Therefore, golden paths that address the challenges of static configuration management have greater potential to optimize a much larger range of processes and at scale.

## Dynamic Configuration Management: The Key to Scalable Golden Paths

Instead of settling for static configuration management, organizations should enable dynamic configuration management (DCM). [DCM](https://humanitec.com/blog/what-is-dynamic-configuration-management) is “a methodology used to structure the configuration of compute workloads. Developers create workload specifications describing everything their workloads need to run successfully. The specification is then used to dynamically create the configuration, to deploy the workload in a specific environment.” With DCM, developers aren’t slowed down by the need to define or maintain any environment-specific configuration for their workloads. DCM drives standardization by design and enables true developer self service.

The Humanitec [Platform Orchestrator](https://humanitec.com/blog/what-is-a-platform-orchestrator), in combination with the workload specification [Score](https://score.dev/), enables DCM by following an RMCD (read, match, create, deploy) pattern: it reads and interprets the workload specification and context, matches the correct configuration templates and resources, creates application configurations and deploys the workload into the target environment wired up to its dependencies. A platform orchestrator is the core of any enterprise-grade IDP because it enables platform teams to enforce organizationwide standards with every git-push.

‍

![](https://cdn.prod.website-files.com/6489e23dd070ba71d41a33b2/65706c86fc28f3d8c4bcbdaf_cRHUC47gFt_z9rbWf_IVqWKVvgeb9_gK0_d44exgTRQn_pLwQRjhyomfq1CukXnJFp_AxBspT3LymKMVscIxJZYbJXNpDlWArQ7IZFJkWBZWN-6pHdOJHvlakdXc_O5MQduYTRJDFRCc7inKjF1-KsI.avif)

## Examples of Scalable Golden Paths

In his PlatformCon 2023 talk, von Grünberg shared a few examples of how a platform orchestrator can facilitate the creation of impactful and scalable golden paths. These examples are also featured in Humanitec’s [IDP reference architecture for AWS-based setups](https://humanitec.com/reference-architectures/aws).

![](https://cdn.prod.website-files.com/6489e23dd070ba71d41a33b2/65706c87b24aaa6825aa5a57_Ww6Mu_uMZv4dMUAgwc4wNB4rs8kUZwZK274C3UpUBViQ9Cl9XobyQ0scPmnvxZLoWSO8jqhuJRngNw3frsQO3Y_C8HyCPPrgw5lDtd1IwjlMTNTphFnsK-8Z6A5nyrnVxFdqkKUeR_PDW2UQbr3Yf7s.avif)

## Simple Deployment to Dev

For example, the golden path pictured below enables developers to deploy the changes made on a workload to dev more efficiently and consistently.

Let’s say a developer wants to deploy a change on their workload to dev. All the developer has to do is modify the workload and git-push to code. From there, the CI pipeline picks up the code and runs it, the image is built and stored in the image registry.

The workload source code contains the workload specificationScore:

![](https://cdn.prod.website-files.com/6489e23dd070ba71d41a33b2/65706c86d64519a9dd148f88_Cn1cSgfpMczXdDIWwXz55SLYfdEy5EsGU-B1fYkHpyT4zIv_4CLPOzHia-MTAWOC17MyQRX5OqT3op8sh4L0OUgGcsaBlWU5a_xMReXNQXGtUEYQHtJGA81dXDVc3uBMJQ5BwJWtbzGJ3UAl2xJpdo0.avif)

In this example, the resources section of workload specification states that the developer requires a database type Postgres, a storage type of S3, and a DNS type of DNS.

After the CI has been built, the platform orchestrator realizes the context and looks up what resources are matched against it. It checks whether the resources have been created and reaches out to 

the AWS API to retrieve the resource credentials. The target compute in this architecture is Amazon Elastic Kubernetes Service (EKS), so the platform orchestrator creates the app configs in the form of manifests. Then the platform orchestrator uses Vault to deploy the configs and inject the secrets at runtime into the container.

![](https://cdn.prod.website-files.com/6489e23dd070ba71d41a33b2/65706c86a961ecbc391a78b8_3Dju-EL9oN0O9Z2IjameuaW3LmyiZ96VlKbKdduNd_-wvfB-aleHRRAww6Js3u8hmrsyA0iiet8N7FCeE43bjzIdrqSBImLTJTVEgmLaSIjYiw25OYcjc_zceGYXypYCudqDR1Nm0B0tZ8l9-yMYUfo.avif)

‍

Deployments like this happen all the time, so optimizing this process makes a major difference for developers and the business at large.

### Create a New Resource

In a static setup, many golden paths fail when faced with a developer request the system is unfamiliar with. With DCM, everything is repository-based, and developers can extend the set of available resources or customize them. 

For example, if a developer needs ArangoDB but it isn’t known to the setup so far, they can add a resource definition to the general baseline of the organization. This way, the developer has easily extended the setup in a way that can be reused by the next developer.

![](https://cdn.prod.website-files.com/6489e23dd070ba71d41a33b2/65706c8718c26531b4308638_NI2k5l8ijKWTiQJfq-YJxCOoLiwYkYS0Qn-_5XniBvdCt0JSkN_IqNxoYeNGkXtaOkWPFNjIr3mG_O-UjUy4Ou1aAQUZBneV-MMeySlQliUc5eurWp5uuvnrPqIXZdPWbjl7ejLkRd9XdPZxEQlRuPU.avif)

### Update a Resource

Updating a resource is a great example of how platform engineers use a platform orchestrator to maintain a high degree of standardization. 

Let’s say you want to update the resource “Postgres” to the latest Postgres version. 

With a dynamic approach to golden paths, the “thing” you need to update is only the resource definition where Postgres is specified.  
  

![](https://cdn.prod.website-files.com/6489e23dd070ba71d41a33b2/65706c86b35544be7d1f84f1_HOAc03FWz_Lo-tBPhR1ex-Be7pD1xcFIzoFgncuA1VcWbVPLZ773lpUOule9-1zqQHM4_AgwNz3k6X-dcdkklhUdWxVL55tUHWKUl8Ssuzocw9wURj9qcbhnMmZ-fifdMa80Nk_QAbgGcCSSbitXMEk.avif)

You can find which workloads currently depend on the resource definition by pinging the platform orchestrator API or looking at the UI in the resource definition section. Once identified, you can auto-enforce a deployment across all workloads that depend on the resource. 

With this golden path, rolling out the updated resource across all workloads and dependencies is simplified and scalable. 

## Good Golden Paths Turn Every Day into Day 1

When platform teams invest in these scalable golden paths, von Grünberg argues, everyone wins. Golden paths that leverage a platform orchestrator and DCM enable developers and ops to execute common tasks with greater ease and peace of mind from the earliest stages of an IDP’s development, delivering more value, faster.

![](https://cdn.prod.website-files.com/6489e23dd070ba71d41a33b2/65706c86fc1bbabab1fc2e9f_fsA4lGTJsGtCOd7ehXbERISvkuX-OdaRMTy3XilEOqdIhC0TgCkghwPL5wBCyykzV_FpaF4PLh6mINTQ3V4PnqeoxGr25wDKlHcy9ZoANwehXFm83UAcph6MF5V-yoKCLs8KpFIIJAgIvYa7oqASirE.avif)

Paving golden paths with this approach also catalyzes an important mindset shift for platform teams, according to von Grünberg. With DCM, every day can become Day 1, a starting point for further optimization and opportunity to reduce technical debt. This shift enables organizations to make the most of what platform engineering has to offer.

![](https://cdn.prod.website-files.com/6489e23dd070ba71d41a33b2/65706c87ded1ccc8e2936a00_yOhTNavpq5cXT5RBgSuMIc1YLmAZhDx7zyKvpE2B66EVW57kEKCHSAYaqZzbRVE_Z_lnmg-TkMxQmKJEz-Km2i9FURQWbCLrAXAfcwbN4PXrCyEpeZXHrG8Defd-tcFHzUAVza9-l7jVe5bCw4I8h3E.avif)

## Get Recommended Golden Path Examples 

Humanitec has created reference architectures for [AWS](https://humanitec.com/reference-architectures/aws), [Azure](https://humanitec.com/reference-architectures/azure), and [GCP](https://humanitec.com/reference-architectures/gcp) based on [McKinsey’s research](https://www.youtube.com/watch?v=AimSwK8Mw-U). These resources walk through examples of recommended golden paths in more detail, as well as how they fit into the larger IDP architecture.