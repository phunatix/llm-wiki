---
title: What are golden paths? A guide to streamlining developer workflows
source: https://platformengineering.org/blog/what-are-golden-paths-a-guide-to-streamlining-developer-workflows
author:
  - "[[Mallory Haigh]]"
published: 2025-01-29
created: 2026-04-23
description: A golden path is a preconfigured, paved road that provides an end-to-end workflow for developers, enabled via an Internal Developer Platform (IDP). It's a predefined route that guides developers through common tasks, designed to reduce cognitive load and ensure that they can operate safely and in compliance.
tags:
  - clippings
  - golden-path
  - developer-experience
---
A golden path is a preconfigured, paved road that provides an end-to-end workflow for developers, enabled via an Internal Developer Platform (IDP). It's a predefined route that guides developers through common tasks, designed to reduce cognitive load and ensure that they can operate safely and in compliance.

[

![](https://cdn.prod.website-files.com/6489e23dd070ba71d41a33b2/688baef6497f5bbf4bf8bb62_mallory-removebg-preview-removebg-preview.avif)

Mallory Haigh

Principal Platform Therapist @ Platform Engineering

](/authors/mallory-haigh)[

Published on January 29, 2025

At the heart of a successful platform engineering initiative lies the concept of the golden path, a meticulously designed and thoughtfully implemented approach to streamlining the software development lifecycle. It’s about creating a smooth, well-lit, and predictable journey for developers, allowing them to focus on what they do best: building innovative and impactful software. Think of it as providing a highway for your developers, enabling them to reach their destinations quickly and efficiently, rather than forcing them to navigate a confusing maze of manual processes. A golden path isn't just a set of tools or technologies; it’s a holistic approach that integrates people, processes, and technology into a cohesive, efficient, and enjoyable experience.

This is how I would define it:

> A golden path is a **preconfigured, paved road that provides an end-to-end workflow** for developers. It's a predefined route that guides developers through common tasks, designed to reduce cognitive load and ensure that they can operate safely and in compliance. The concept of a golden path is also referred to as a "happy path" in software engineering. Golden paths are a key component of an Internal Developer Platform (IDP).”

A golden path, at its core, is a predefined, end-to-end workflow that guides developers through common tasks, such as provisioning infrastructure, deploying applications, and managing configurations. This path is not merely a suggestion; it’s a thoughtfully crafted route designed to abstract away the complexities of the underlying infrastructure, allowing developers to focus on their primary skillset of writing code. It is built upon the foundation of standardization and automation, creating consistent, repeatable processes that reduce the risk of human error and promote operational efficiency. This means that tasks are performed uniformly, no matter who is doing them, ensuring that the entire development process is more predictable and reliable.

A crucial aspect of a golden path is its focus on self-service capabilities. This means that developers can autonomously use the platform to perform tasks without the need for constant interaction with operations or infrastructure teams. This self-service approach significantly accelerates development cycles, reducing wait times and empowering developers to move faster. It gives them the keys to the car, so they can go where they need, when they need to go there, without needing to request a ride.

![](https://cdn.prod.website-files.com/6489e23dd070ba71d41a33b2/679a66877480b3f8261be05f_AD_4nXfmX_fPW5cxFu6jEnCfzedMkGsMjgkfrqyM0FLVIAC4kXTd8GETwwsSL8QYJ-v7YKPBSUd_XwxiBRTus15fX9trl5MkdADndd-02dbWoA2nC1sOeMG0Slin2oTB6ofJcgoRRvq6.avif)

However, a golden path is not intended to be a rigid, inflexible constraint. While it provides a well-trodden and optimized route, it should also allow for developers to deviate when necessary. The goal is not to create a "golden cage," but rather to provide a "golden path" - a helpful and efficient way of doing things that enables innovation and creativity. The platform should also be designed in a way that facilitates discovery, so that when developers go off the path, new requirements or needs can be identified and potentially standardized into new golden paths.

## Why golden paths matter

The adoption of golden paths within an organization is essential for several key reasons:

- **Reduced cognitive load:** Developers are often burdened with the complexities of managing infrastructure, deployments, and security configurations. Golden paths abstract this complexity, allowing developers to focus on their core competency: writing code. By simplifying these processes, developers can operate with less cognitive load, enabling them to be more productive and creative.
- **Improved consistency and reliability:** Standardized, automated workflows ensure that tasks are performed consistently, reducing errors and improving overall system reliability. When processes are uniform, it becomes easier to troubleshoot issues and maintain system health. This can be compared to having a well-organized assembly line; when each step is the same every time, it’s easier to produce a consistently high-quality product.
- **Faster development cycles:** Self-service capabilities empower developers to move faster, reducing wait times and accelerating the overall development process. By eliminating the need for constant back-and-forth communication between teams, golden paths streamline workflows and enable faster iteration. It reduces the amount of time that developers need to spend waiting on infrastructure or other team members and allows them to proceed with development on their own terms.
- **Enhanced security and compliance:** Golden paths incorporate security best practices into the workflow, ensuring that all operations are safe and compliant. By defining pre-approved paths for security configurations, it becomes easier to reduce vulnerabilities and adhere to industry regulations, allowing security teams to easily enforce rules, but also providing a seamless security experience for the developers.
- **Increased developer satisfaction:** By providing a smoother, more streamlined experience, golden paths significantly improve developer satisfaction. When developers feel empowered and unburdened by operational complexities, they are generally more engaged and productive. It’s about making the day-to-day experience of development less frustrating and more enjoyable.

## Building effective golden paths

### Key considerations

When building golden paths, there are a few additional considerations to keep in mind:

- **"Vending machine" mentality:** Platform engineering can be thought of as a "vending machine" where platform engineers make available their products for developers to consume. Developers can select what they need and the platform will provide a uniformly delivered product.
- **Metrics and Measurement:** It is important to measure the status quo before implementing any golden paths, then gather data after implementation. This will be important for demonstrating value through quantifiable metrics, such as reduced onboarding time, increased deployment frequency, and improved developer satisfaction. The measurement of success is something that should be started from the beginning and include both leading indicators, as well as lagging indicators. These metrics can help to refine and improve the platform over time.
- **Adoption:** A key aspect of implementing golden paths is ensuring they're easily adopted by the development teams, which means giving developers the freedom to use the interfaces and workflows they are most comfortable with, whether that's a GUI, a CLI, an API or code-based via a workload specification like [Score](https://score.dev/).
- **Iterative approach:** The development of a golden path should follow an iterative approach, starting with a [Minimum Viable Platform (MVP)](https://platformengineering.org/blog/what-is-a-minimum-viable-platform-mvp) and building on it as the needs of developers evolve. This approach makes it easier to provide value quickly and to incorporate feedback.

### **Design steps to build your golden paths**

1. **Identify pain points:** Use value stream mapping to visualize the steps, lead times, process times, and completion rates of a workflow. Break down processes into granular tasks to identify the biggest pain points.
2. **Map current state**: Analyze the current setup and workflows. This involves understanding the flow of a task, the different people involved, and the interaction points.
3. **Define the ideal state**: Design the ideal workflow, considering the target personas (developers, operations, security) and their needs. Determine the most ideal scenario for the workflow to function.
4. **Prioritize impact**: Focus on the golden paths that will have the most impact. Consider the frequency of the task and the amount of time spent on it. Prioritize tasks that are done most often.
5. **Incorporate abstraction**: Provide the right levels of abstraction through front end and back end systems. Developers will have different needs and preferences in how they interact with the platform.

### Examples of golden paths

Golden paths can be applied to various aspects of the software development lifecycle. Here are some examples:

- **Provisioning a database:** A developer can request a database, such as Postgres, through a UI or code-based interface, without needing to worry about the underlying configurations.
- **Scaffolding a new service**: This involves setting up the initial structure of a new application. A golden path here might involve multiple teams such as developers, security, and operations.
- **Automated environment progression**: This is where the deployment process between environments (development, staging, production) is automated. A git push, for example, can trigger automated policy checks and sign-offs.
- **Updating app configurations**: A golden path would allow developers to modify environment variables quickly and easily.
- **Adding services and dependencies**: A streamlined way for developers to add and manage the services and other dependencies required for their applications.
- **Spinning up ephemeral environments:** Developers can quickly spin up temporary environments through a golden path. For example, a simple Git push can trigger the creation of a new environment.
- **Adding an S3 bucket**: Developers can add an S3 bucket to an existing workload with just a couple lines of code.
- **Understanding the difference between deploy A and B, then roll back:** This path simplifies the process of comparing two deployments and allows developers to roll back with one click.
- **Running policy checks and security sign-offs:** A golden path would enable the integration of automated policy checks and human security sign-offs into the deployment process.

On internaldeveloperplatform.org you can find more examples and some calculations to estimate the value of golden paths:

![](https://cdn.prod.website-files.com/6489e23dd070ba71d41a33b2/679a6687b3b258345d4dca8e_AD_4nXfiuTMMQ1cf2tex7Fl0AWSiKjs11FhvPy9G4nkZtJFq9X53I3W0IvdCxYSUTapJS2oN_PJu4fL0kbjh0QUVoJdeGsVULsXHe4gm7Jt-Y5bsXsaVOMtszPjXM2y0luq_LQ.avif)

### The importance of day-to-day operations

When designing golden paths, it's essential to focus on day-two operations, which are the day-to-day tasks that developers perform. These tasks, when done manually, can add up to a lot of wasted time and resources. Golden paths should address these pain points and be built around the things that will have the most impact. Examples include daily deployments with configuration changes, spinning up ephemeral environments, adding or updating resources, and scaffolding.

## Moving forward with golden paths

Golden paths aren't just about making things easier; they're about creating a more productive, efficient, and enjoyable experience for developers. They are also an essential piece of a broader platform engineering initiative, a key to building high-performing software development organizations. By creating the right golden paths, and following a structured, iterative approach, you can guide your developers to build better software, faster. In order to be successful, platform engineering teams must always be listening to their customers: the developers, operations, and security teams, and using that information to further refine and improve the golden paths available on the platform. By doing this, golden paths can be used to make the lives of developers and other engineers easier.