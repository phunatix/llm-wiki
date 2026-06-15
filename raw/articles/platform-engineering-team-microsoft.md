---
title: "Build the Platform Engineering Team"
source: "https://learn.microsoft.com/en-us/platform-engineering/team?source=recommendations"
author:
  - "[[juliakm]]"
published:
created: 2026-06-15
description: "Learn about the role of platform engineers as the bridge between development and operations, and why you need a team with diverse skill sets."
tags:
  - "clippings"
---
## Build your team

At an organizational level, platform engineering is an evolution away from reactive culture. In a reactive culture, lone developers build tools in silos. When that one developer leaves, the knowledge of how that tool works leaves as well, which can lead to broken processes and downtime.

In a more mature culture, tools are built proactively and maintained by the platform engineering team. There's managed autonomy for developers, and developers can quickly get started on new projects.

For platform engineering teams to succeed, their organizations need to have proactive cultures with executive buy-in and developers with the right skills.

Proactive culture and executive buy-in aligns with the [investment capability](https://learn.microsoft.com/en-us/platform-engineering/investment) in the [Platform Engineering Capability Model](https://learn.microsoft.com/en-us/platform-engineering/platform-engineering-capability-model). At the highest levels, company leadership promotes team autonomy and accountability while encouraging innovation and implementing governance measures.

## Role of culture

Organizations with platform engineering maturity have strong leadership. Platform engineering within a company is a balancing act that requires continuous reassessment. Organizations need to support the platform engineering team in its efforts to understand current resource usage and map a path forward.

In the early stages of platform engineering adoption, product teams each have their own unique set of tools, operations, and deployment processes. In a mature platform engineering organization, centralized platform engineering is viewed as the best way of working by both leadership and developers. Mature organizations recognize that product team issues are organizational problems.

> ..when we were chasing down different paths, the cloud cost, infrastructure cost, engineering cost, various aspects, it turned out to be an organizational problem and everybody's problem of 20,000 developers or 30,000 employees of the organization problem. – *Senior engineering leader at an enterprise software company*

Your organizational culture needs to support being on a constant discovery path in platform engineering. Executives should focus on empowering the platform engineering team to innovate.

The goal for your organization should be to move toward an optimizing culture where executives:

- Empower teams to address edge cases effectively and drive innovation.
- Promote autonomy and accountability within teams to encourage innovation and experimentation.
- Ensure continual relevance and effectiveness amid evolving business needs and user demands.

Over time, organizations move from the provisional to optimizing levels of supporting cultural changes with platform engineering. At each level, leadership's role evolves in order to drive the cultural changes necessary to embrace the vision of platform engineering.

| Provisional | Operational | Scalable | Optimizing |
| --- | --- | --- | --- |
| Drive a culture of data-driven decision making and adaptability. | Promote a culture of collaboration, continuous learning, and improvement. | Promote a culture of empathy and growth. | Encourage innovation and empower teams to drive change and progress. |

Organizational motivations also evolve at each level to support platform engineering cultural change.

| Provisional | Operational | Scalable | Optimizing |
| --- | --- | --- | --- |
| - Recognize the imperative to implement an organization-wide solution. - Prioritize obtaining insights into inefficiencies using metrics and measurements to effectively pinpoint system bottlenecks. - Enhance organizational structure to enable and support change initiatives. | - Cultivate a collaborative mindset across the organization to promote collective problem solving. - Prioritize the establishment of robust feedback mechanisms to drive continuous improvement. - Promote a culture of reliability. | - Drive a product-led growth approach to achieve sustainable success. - Foster a culture of empathy and a growth mindset among teams. - Elevate the importance of product user research in decision-making processes. | - Empower teams to address edge cases effectively and drive innovation. - Promote autonomy and accountability within teams to encourage innovation and experimentation. - Ensure continual relevance and effectiveness amid evolving business needs and user demands. |

## Organization structure

Platform engineers are the glue between development and operations. In terms of specific organization structure, the [Team Topologies model](https://teamtopologies.com/key-concepts) is a good approach to think about what you need to do. For example, you might opt to have an evolved platform team, with separate specialists that are more focused on the developer facing aspects of your platform.

To be successful, identify:

- Sponsors for the team (typically executives) who help with prioritizing high-level goals and championing the platform's use across the wider organization.
- Stakeholders from operations, security, compliance, and architecture to help ensure that the platform can accommodate their guidance and needs.
- Someone to act as the product manager (regardless of actual title) to understand and help prioritize needs from all constituents.

## Overcome the talent gap: platform engineer requirements

Platform engineers need to have a product mindset and also understand operations. Whether they started out as developers or on the operations team is less important than skill set. A team building an internal developer platform can gain strength from bringing in various team members with different backgrounds: development, IT operations, Kubernetes admins, site reliability engineers (SRE), and infrastructure as code (IaC) experts.

You can also strengthen your team’s knowledge and skill set for developing tools by bringing well-suited developers from existing application teams in your organization. These developers are in a good place to help represent the voice of the customer as you think about your investments.

Finding platform engineers can be a challenge.

> It's very difficult to hire really good infrastructure and platform engineers. Many of the people we hire today are super passionate about the applications that are directly customer facing, right? But we don't have a big audience or candidates in the entire tech industry that are passionate about infra engineering and that's always a challenge...For infra, this kind of expertise is rare. - *VP of engineering at a medium-size sales company*

Platform engineers should be able to:

- Build and scale internal developer products with focus on efficiency, reliability, and security.
- Contribute to the architecture and design of the platform engineering products.
- Work successfully with container orchestration (for example, Kubernetes), continuous integration and continuous deployment (for example, GitHub Actions, Azure Pipelines), and monitoring and logging tools (for example, Prometheus, Grafana, Elasticsearch).
- Build templates with infrastructure as code and associated tools (for example, Terraform and Azure Resource Manager).
- Write code in at least one scripting language (for example, Python, PowerShell, and Bash).

Building a great platform engineering team requires a blend of diverse technical skills and a product-centric approach. Despite the hiring challenges, building a team with varied backgrounds leads to better internal platforms that improve efficiency, reliability, and security. This holistic approach not only addresses your organization's immediate technical needs but also fosters a culture of innovation and continuous improvement.

## Next step

[Define the problem space](https://learn.microsoft.com/en-us/platform-engineering/problem-space)

---

## Additional resources

Training

Module

[Foundations of Platform Engineering - Training](https://learn.microsoft.com/en-us/training/modules/foundations-platform-engineering/?source=recommendations)

This module introduces the core concepts and importance of platform engineering. It explores how platform engineering enhances developer productivity, accelerates time to value, and supports digital transformation. Learners will understand the strategic value of platform engineering as the foundation for both technical success and alignment with broader business goals.

Certification

[Microsoft Certified: DevOps Engineer Expert - Certifications](https://learn.microsoft.com/en-us/credentials/certifications/devops-engineer/?source=recommendations)

This certification measures your ability to accomplish the following technical tasks: Design and implement processes and communications, design and implement a source control strategy, design and implement build and release pipelines, develop a security and compliance plan, and implement an instrumentation strategy.