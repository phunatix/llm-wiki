---
title: "Platform Engineering Maturity Model"
source: "https://tag-app-delivery.cncf.io/whitepapers/platform-eng-maturity-model/"
author:
published:
created: 2026-04-10
description: "This maturity model intends to provide tactical guidance to users seeking to adopt the patterns discussed in the Platforms Definition White Paper. That paper suggests why and what to build; this document will begin to describe how to plan to build it. The target audience is CTOs, Directors of engineering, lead engineers, and architects seeking to evaluate their current state and environment and identify opportunities for improvement.<br/><br/> This document refers to, enhances, and follows similar standards as the following related documents:<br/> [Cloud Maturity Model](https://maturitymodel.cncf.io/)<br/> [Platforms Definition White Paper](https://tag-app-delivery.cncf.io/whitepapers/platforms/)"
tags:
  - "clippings"
---
## Introduction

CNCF’s initial [Platforms White Paper](https://tag-app-delivery.cncf.io/whitepapers/platforms/) describes what internal platforms for cloud computing are and the values they promise to deliver to enterprises. But to achieve those values an organization must reflect and deliberately pursue outcomes and practices that are impactful for them, keeping in mind that every organization relies on an internal platform crafted for its own organization - even if that platform is just documentation on how to use third party services. This maturity model provides a framework for that reflection and for identifying opportunities for improvement in any organization.

## What is platform engineering?

Inspired by the cross-functional cooperation promised by DevOps, platforms and platform engineering have emerged in enterprises as an explicit form of that cooperation. Platforms curate and present common capabilities, frameworks and experiences. In the context of this working group and related publications, the focus is on platforms that facilitate and accelerate the work of [internal users](https://tag-app-delivery.cncf.io/wgs/platforms/glossary/#platform-users) such as product and application teams.

[**Platform engineering**](https://tag-app-delivery.cncf.io/wgs/platforms/glossary/#platform-engineering) is the practice of planning and providing such computing platforms to developers and users and encompasses all parts of platforms and their capabilities — their people, processes, policies and technologies; as well as the desired business outcomes that drive them.

Please read the [CNCF Platforms White Paper](https://tag-app-delivery.cncf.io/whitepapers/platforms/) first for complete context.

## How to use this model

As platform engineering has risen in prominence over the last few years, some patterns have become apparent. By organizing those patterns and observations into a progressive maturity model, we aim to orient [platform teams](https://tag-app-delivery.cncf.io/wgs/platforms/glossary/#platform-team) to the challenges they may face and opportunities to aim for. Each aspect is described by a continuum of characteristics of different teams and organizations at each level within the aspect. We expect readers to find themselves in the model and identify opportunities in adjacent levels.

Of note, each additional level of maturity is accompanied by greater requirements for funding and people’s time. Therefore, reaching the highest level should not be a goal in itself. Each level describes qualities that should appear at that stage. Readers must consider if their organization and their current context would benefit from these qualities given the required investment.

Keep in mind that each aspect is meant to be evaluated and evolved independently. However, as in any socio-technical system these aspects are complex and interrelated. Thus you may find that to improve in one aspect you must reach a minimum level in another aspect too.

It’s also important to recognize that implementations of platforms vary from organization to organization. Make sure to evaluate the current state of *your* group’s overall cloud native transformation. A phenomenal resource to leverage for this evaluation is the [Cloud Native Maturity Model](https://maturitymodel.cncf.io/).

Finally, this model encourages organizations to mature their platform engineering discipline and their resulting platforms through intentional planning. Such planning and discipline themselves are a requirement for mature platform development and ongoing evolution.

In general, keep in mind that mapping your organization into a model captures current state *to enable* progressive iteration and improvement. [Martin Fowler](https://martinfowler.com/bliki/MaturityModel.html) says it well: “The true outcome of a maturity model assessment isn’t what level you are at but the list of things you need to work on to improve. Your current level is merely a piece of intermediate work in order to determine that list of skills to acquire next.” In that vein, seek to find yourself in the model then identify opportunities in adjacent levels.

## Context behind this work

It’s valuable to understand the context a document has been written in. The following sections lay out some context behind the model as well as some expectations for you, the reader.

### Intended audiences

Each reader brings a unique context and will take unique learnings from this model. Following are some personas we have in mind, along with their possible motivations for engaging with this model:

- **CTOs, VPs, and directors of technology**: Leaders looking to map a path to digital transformation and greater developer productivity
- **Engineering managers**: Groups and individuals seeking to empower engineers to provide value with less overhead and higher efficiency
- **Enterprise architects**: Individuals navigating the modern technology landscape who seek a value- and solution-oriented perspective on technology problems
- **Platform engineers and platform product managers**: Teams and people seeking to build the best possible experience for platform builders and platform users
- **Product vendors and project maintainers**: Organizations and engineers wishing to design tools and deliver messages to enable users to succeed with platforms and capabilities
- **Application and product developers**: Platform users seeking to understand in more detail what they might expect of an internal platform

### Understanding the levels

This model is not meant to classify an organization or platform team as wholly “Level 1” or “Level 4.” Each aspect should be considered independently of the others; the characteristics of each level represent a continuum within that aspect but are not necessarily coupled to other aspects at the same level. Even more so, many organizations will see characteristics of more than one level being applicable across their teams and work. This is because no level is inherently good or bad, only contextual to the team’s goals.

The labels for each level are intended to reflect the impact of platform engineering at your organization. As you recognize your organization at a given level you will gain insight into opportunities which follow at the next ones. Lower-numbered levels comprise more tactical solutions while higher-numbered ones are more strategic.

This yields a potential process for platform development and maturity similar to other digital product development: first recognize a problem and need for a new solution, next develop minimally-viable products as hypothesized solutions, third iterate to better solve the problem and ensure fit for your customers and finally scale and optimize the product to solve the problem for many teams and users.

Similar to the [CNCF Cloud Native Maturity Model](https://maturitymodel.cncf.io/), this model highlights that successful business outcomes can only be achieved through balancing people, process, and policy alongside technology. Notably, this model introduces aspects which are often not fully in the remit of a single internal team, but rather require cooperation across the engineering department and quite often the wider organization.

### But it doesn’t seem to fit

That’s perfectly fine! All organizations and groups have dynamics and parameters that are specific to them.

Keep in mind that the goal of this paper isn’t to prescribe a rigid formula, but rather a framework that you can apply to your circumstances. Every single word may not be relevant to you, but we hope the content will inspire you to introspect on your own platform journey, taking what makes sense and leaving the rest.

The objective of this model is to provide a tool to help guide platform engineering practitioners, stakeholders, and other interested parties on their journeys. Platform design and implementation is not an exact science, but rather depends on the needs of an individual project, an organization and a particular time and place.

## Model table

| Aspect |  | Provisional | Operational | Scalable | Optimizing |
| --- | --- | --- | --- | --- | --- |
| [Investment](#Investment) | *How are staff and funds allocated to platform capabilities?* | Voluntary or temporary | Dedicated team | As product | Enabled ecosystem |
| [Adoption](#Adoption) | *Why and how do users discover and use internal platforms and platform capabilities?* | Erratic | Extrinsic push | Intrinsic pull | Participatory |
| [Interfaces](#Interfaces) | *How do users interact with and consume platform capabilities?* | Custom processes | Standard tooling | Self-service solutions | Integrated services |
| [Operations](#Operations) | *How are platforms and their capabilities planned, prioritized, developed and maintained?* | By request | Centrally tracked | Centrally enabled | Managed services |
| [Measurement](#Measurement) | *What is the process for gathering and incorporating feedback and learning?* | Ad hoc | Consistent collection | Insights | Quantitative and qualitative |

## Model Detail

  

---

## Conclusion

Platforms and their maintainers provide a foundation for agile digital product development. They provide a consistent collection of capabilities that enable efficient software development and delivery. This maturity model provides a map for your platform engineering journey.