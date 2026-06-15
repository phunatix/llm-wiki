---
title: "Design a Developer Self-Service Foundation"
source: "https://learn.microsoft.com/en-us/platform-engineering/developer-self-service"
author:
  - "[[juliakm]]"
published:
created: 2026-06-15
description: "Learn how to build or evaluate products that create a flexible foundation for your developer self-service experience."
tags:
  - "clippings"
---
Once you have a good understanding of your target for your [engineering systems](https://learn.microsoft.com/en-us/platform-engineering/engineering-systems), you can create more sophisticated developer self-service experiences. A developer self-service experience is built on a foundation of concepts, patterns, and components.

While you might not need everything described here in your organization today, you should keep these concepts in mind if you build something custom or evaluate related products. Your developer self-service experience model can be made up of a combination of home-grown, off-the-shelf, and open-source products. Products or open-source portal toolkits like [Backstage.io](https://backstage.io/) might use different terms for some elements of the model described here, but the model can still help orient you.

## Automate workflows, aggregate data, start simple, and expand gradually

Your goal is to enable self-service with guardrails through controlled, governed task execution and provisioning, along with centralized visibility. The areas that are the most valuable to focus on are those that are either tedious or are things the developer can't do themselves due to complexity or permissions. This last piece is important to allow you to follow the principle of least privilege without forcing developers through a manual service desk process.

While you can opt to extend your DevOps suite to meet these needs, you'll likely need to support multiple [application platforms](https://learn.microsoft.com/en-us/platform-engineering/application-platform) over time, and the specific tools and processes that support them might need to change as well. The core issue is that your standards are a moving target. As one platform engineering practitioner stated:

> The difficulties involve standardization … and dealing with 'abandonware'… Standardization is often not achieved due to potential disruption of automated processes and the time-consuming task of identifying necessary changes. - *Martin, DevOps engineer, large logistics company*

Rapidly switching to a new or updated standard is typically not feasible, and abandoning existing processes creates risk. Your organization might already be using multiple DevOps suites or different combinations of individual tools and developer services by scenario. Even with a central team and a standard solution, as your self-service needs increase, variability is inevitable. So, you'll want to allow controlled experimentation where designated teams might try out new technologies, deployment strategies, and so on, followed by deliberate adoption and an incremental rollout.

Generally self-service experiences fall into two primary categories: automation and data aggregation.

While data aggregation creates good user experiences, automation is more important:

> Automation is key and will be loved by everyone. \[Data\] aggregation is secondary. – *Peter, platform engineering lead, multinational tech company*

In your [platform engineering journey](https://learn.microsoft.com/en-us/platform-engineering/journey), you identified problems potentially solved by automation. Beyond reducing cognitive load and developer toil, automation also can help ensure applications are connected into the best tools and services for operations, security, and other roles to do their work.

However, if you work with more than one system to drive your automation, some level of data aggregation is useful to help track of automated requests and the associated results. You can start by linking to external systems to meet other needs or for drill-in on details. Data aggregation and visibility is also important to auditing, governance, and reducing waste (for example, unused environments).

Automating things like infrastructure provisioning can be done using system integrations, but you can also trigger and facilitate a manual workflow process that looks automated to the developer. This is useful in the early stages of your platform, for new products you're bringing into your ecosystem, or in areas you haven't or can't automate using a system (for example, software license assignment). With the right design, you can start with a manual process facilitated by something like Power Automate that you switch over to a fully automated flow over time. So, design for an automation from the start.

Start simple by reusing existing investments like your engineering systems or an internal portal, then move to creating CLIs, basic web pages, or even [Power Pages](https://learn.microsoft.com/en-us/power-pages/), [Power BI](https://learn.microsoft.com/en-us/power-bi/), or [Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/) dashboards, and expand as the need arises. Having a consistent API that UX then uses can help you support multiple interfaces over time as your needs and preferences change.

## Developer self-service platform components: API, graph, orchestrator, providers, and metadata

Consider the foundations of developer self-service:

![Diagram of the foundations of developer self-service.](https://learn.microsoft.com/en-us/platform-engineering/media/self-service-foundation.svg)

Diagram of the foundations of developer self-service.

As the illustration shows, the following components make up the core of the concept of a developer self-service foundation:

| Component | Description |
| --- | --- |
| Developer platform API | Your single point of contact for user experiences. It's effectively the system’s contract with other systems. |
| Developer platform graph | A managed and secure data graph that allows you to discover, associate, and use different kinds of entities and templates. An entity is an object that enables data aggregation from multiple sources, while templates drive user inputs that enable automation. |
| Developer platform orchestrator | A capability that routes and tracks template-based requests to perform actions either in a system or through a manual process. These requests are routed to one of a set of developer platform providers that can integrate to any number of different workflow systems or other services. |
| Developer platform providers | A set of components that encapsulate logic needed to integrate with downstream systems to support CRUD operations on entities or fulfillment of template-based action requests. Each provider can support its own specific type of templates and emit either unique or common types of entities. |
| User profile and team metadata | A capability to persist information about a set of individuals tied to a conceptual team for grouping and access to the developer platform API. The user is closely associated with an identity provider account (for example, Microsoft Entra ID sign in), but both it and a team can tie to any number of related downstream system representations. One implementation of this information store is to reuse the developer platform graph. The developer self-service foundation can establish a common entity type for both a user and a team and persist that information in the graph. However, we'll keep this store separate for the sake of clarity here. |

These foundational components enable you to use and swap out different building blocks over time.

### Do I have to build all of this to get started?

No. First, this is a conceptual model to help you think through what a foundation like this should be able to do once it's done. Second, the implementation specifics are less important here given the developer platform API becomes your key interface. Your initial implementation might start out using interfaces and classes in your code for the different layers described or mix in other products. You could also omit aspects because your customer development tells you it's simply a lower priority. Start with what you have and grow.

### Developer platform API

You should define a developer platform API to act as your system’s contract. The API is used by different user interfaces to enable data access or drive provisioning and other actions.

This API acts as an important authentication and security layer by limiting access to raw underlying APIs in other systems to more specific, controlled data and operations. The API provides access to its own representation of a user profile, a user's high-level role within the platform (team member, admin, etc.), and primary identity provider system identifiers. For more information, see [Users and teams](#users-and-teams).

## Developer platform providers

Given the breadth of an internal developer platform, you should create or identify systems that follow an extensible provider model to introduce functionality into the API. The idea is that key functionality like automation and data aggregation is provided by interacting with pluggable components with well-defined interfaces. This loose coupling helps you wire in what you need incrementally and improves maintainability since you can test functionality independent of the rest of the foundation.

It’s also an important way to enable a scalable [inner source](https://innersourcecommons.org/) mentality for your platform. Typically, inner sourcing efforts around platform engineering fail to gain traction due to challenges with ongoing maintenance. Other teams might be willing to contribute functionality but are less likely to be willing to maintain and test something inside the core of your platform. Conversely, any centralized team has limited capacity to maintain contributed code or even review pull requests. The concept of a developer platform provider alleviates this tension by allowing independently written code to *plug in* to core functionality within your developer self-service foundation. Though you should carefully manage which the providers you use, review any provider code, and limit the surface area that a given provider can access in your developer platform, a pluggable approach can help you get more done by scaling the effort across a broader portion of the organization.

### Key developer platform provider concepts

#### Entities

The concept of an entity is something that a developer or other system in your internal developer platform needs to track, update, present, or act on. Entities can have relationships with one another that, when taken together, make up a [graph](https://en.wikipedia.org/wiki/Graph_\(discrete_mathematics\)) that provides critical information about pieces of your internal developer platform. Developer platform providers can then output entities to enable core capabilities, including:

- Surfacing externally provisioned resources / environments or available APIs for discovery and use
- Exposing relationships for dependency analysis, impact analysis, discovery, etc.
- Surfacing maintainer / ownership information for discovery and collaboration
- Surfacing more data for use in user experiences

Encapsulating this functionality into a well-defined developer platform provider interface simplifies integration and testing, enables independent deployment, and allows developers outside of the primary internal developer platform team to contribute and manage providers. This is important in large or divisional organizations where not every tool, service, or platform is managed centrally, but the broader organization still wants to share capabilities. So, even if you don't head down this path initially, it's something to think about over the long term.

#### Common properties

Each entity should have a set of common properties to allow the foundation to manage them. Some properties to consider include:

- Unique identifier
- Name
- Originating provider
- Optional associations to:
	- Owning user
		- Owning team
		- Other entities

The user and team properties are important for three reasons: role-based access control (RBAC), discovery, and data aggregation (such as team level summaries). Incorporating RBAC from the beginning is critical to security and growing your internal developer platform over time. Given development is a team sport, discovering who to talk to about an entity will quickly become critical for reuse, support, and innersourcing.

#### Common and provider-specific entities

You should also be able to establish a set of common high-level, normalized entities that multiple providers can output. For example:

- Environments
- Resources
- APIs
- Repositories
- Components
- Tools

These generally should be at a high level, like you would place in [C4 model context](https://c4model.com/#SystemContextDiagram) or at most high-level [component diagrams](https://c4model.com/#ComponentDiagram). For example, for an environment, you don’t need to include the details of the internal infrastructure topography; you just need enough information to list and associate different conceptual environments from multiple providers in the same UX. The entity can point to lower levels of detail outside off the system rather than trying to consume everything. These provide starting points for discovery that are is central to enabling data aggregation over time.

Others are specific to a particular use case or provider, so you should think about how you can accommodate a growing set of entity types over time.

#### Templates

The concept of a template in this context differs from the idea of entities in that they're intended to drive an action. Example scenarios include infrastructure provisioning, creating a repository, and other long-running processes. These templates should also be available through extensible developer platform providers and should support the same common properties as entities, including entity associations.

However, they can also define required inputs, whether system or user specified, that are needed to perform the action. These can range from anything like naming the resource to optional additions.

Examples of templates include:

- [Infrastructure as code (IaC) templates](https://learn.microsoft.com/en-us/platform-engineering/engineering-systems#enable-automatic-application-infrastructure-provisioning-during-continuous-delivery)
- [Application templates](https://learn.microsoft.com/en-us/platform-engineering/engineering-systems#create-start-right-application-templates-that-include-stay-right-configuration) (start right) or template repositories
- Build pipeline / workflow templates
- Deployment pipeline / workflow templates
- Parameterized scripts
- Parameterized [Power Automate](https://learn.microsoft.com/en-us/power-automate/) flows (for example, an HTTP request triggered cloud flow)
- Email templates

Like entities, templates can include provider-specific properties.

Each template might have a different representation that's unique to the provider. These might range from Terraform or ARM templates, to Helm Charts, parameterized GitHub Actions workflows or Azure Pipelines, simple scripts, or custom formats.

The actual underlying template details don't necessarily need to be stored centrally. They could exist in different repositories, registries, or catalogs. For example, you could use [GitHub template repositories](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template) for your application templates, while your IaC templates might exist in a restricted catalog repository that developers can only indirectly access through something like [Azure Deployment Environments](https://azure.microsoft.com/products/deployment-environments/). Other IaC templates might be stored in an OCI Artifact Registry like Helm charts. In other cases, the template might be a reference to a parameterized HTTP endpoint. A developer platform provider should provide enough information about each type of template so that they can be referenced, and any options exposed for use in user experiences. But, the templates themselves can be housed in the most natural location for your use cases.

Platform engineers or experts on a particular area write templates and then share them with development teams for reuse. Centralizing the use of these templates through a system allows developer self-service and creates guardrails that help enforce compliance with organizational standards or policies. More on this when we cover the developer platform orchestrator in a bit.

## Developer platform graph

You can think of a developer platform graph as something that allows you to associate entities and templates from multiple providers into a searchable graph. However, the actual data for the entities doesn't necessarily need to be persisted directly in a graph-specific database. Instead, interactions with providers could be cached along with needed metadata to make it all fit together.

![Diagram of developer platform graph including providers and orchestrator.](https://learn.microsoft.com/en-us/platform-engineering/media/developer-platform-graph.svg)

Diagram of developer platform graph including providers and orchestrator.

The graph is powerful when used with common entities that multiple providers could contribute. For example, a list of APIs might come from a product like [Azure API Center](https://learn.microsoft.com/en-us/azure/api-center/), but you might also want to automatically feed in deployments and environments from your continuous deployment systems. Over time, you could switch between different deployment systems or even support more than one deployment system. So long as each deployment system has a developer platform provider, you should still be able to make the association.

Each of your user experiences that build up from this graph can then take advantage of a common API to power discovery, search, governance, and more. A developer platform orchestrator can then take advantage of this same graph so that any actions performed by a developer platform provider automatically contribute entities available to the same API.

## Developer platform orchestrator

A developer platform orchestrator allows developers or systems to create requests to perform an action using a template. It doesn’t perform these actions itself, but instead coordinates with a task engine, workflow engine, or another orchestrator to do so. It's one of the critical pieces you'll want to be sure is a part of your self-service foundation. It allows developers to create requests with a template or execute an action without direct permission. Furthermore, unlike the concept of CI or CD, these actions don't have to be related to application source code.

You could use GitHub Actions, Azure Pipelines, or another workflow engine as your orchestrator. This is a reasonable place to start, but you might want to have a bit of abstraction in place to allow different types of templates to use different underlying engines. This can be useful for a few reasons:

- First, you'll likely want to be able to pick different workflow and task execution engines over time without having to [flash cut](https://en.wikipedia.org/wiki/Flash_cut). By allowing more than one engine, you can migrate over time or simply the use of the new engine to new actions without impacting older ones.
- Some processes you want to help orchestrate might require manual steps initially even if you plan to fully automate them later.
- Others action might target roles outside of the dev team like accounts payable or a license admin. Low-code engines like Power Automate often work well for these roles.
- Other actions might be handled through simple HTTP requests where spinning up something as capable as [GitHub Actions](https://docs.github.com/actions) or [Azure Pipelines](https://learn.microsoft.com/en-us/azure/devops/pipelines/) isn't necessary or cost effective to scale.

Fortunately, expanding on the idea of a developer platform provider to cover triggering and tracking automation steps can provide this needed abstraction. Consider the following illustration:

![Diagram of platform orchestrator with developer platform API and entity provider routing and handing.](https://learn.microsoft.com/en-us/platform-engineering/media/platform-orchestrator.svg)

Diagram of platform orchestrator with developer platform API and entity provider routing and handing.

Here’s the general concept:

- Templates can optionally specify a set of inputs that the user can enter. When a developer triggers a particular action, they pick a template (even if not described that way) and enter any inputs.
- A reference to the template-related inputs becomes a request in the developer platform API.
- Once a request is submitted, a request routing and handling component within the orchestrator begins tracking the lifecycle of the request. The request routing and handling component routes template in the request to the developer platform provider where the template originated.
- The developer platform provider then performs the appropriate steps for its implementation.
- (Optional) The developer platform provider updates the request status as it performs the action.
- Once the request is fulfilled, the developer platform provider can return a set of entities to add or update in the developer platform graph. These could be provider specific or common entities.

Optionally, to support more advanced interactions, developer platform providers can call the developer platform API directly to either get more entities as inputs or even request another related action.

Pick a developer platform provider that uses a general task or workflow engine. More specifically, you want something to bridge what you put together as a part of [Apply software engineering systems](https://learn.microsoft.com/en-us/platform-engineering/engineering-systems). One general workflow or task execution engine to invest in is a CI/CD system.

### An example using GitHub Actions or Azure Pipelines

Let's briefly look at how a GitHub Actions or Azure Pipelines as a developer platform provider would work.

For GitHub Actions, the key to making this work is that a developer platform provider can connect to the specified GitHub instance and use the [Actions REST API to fire a workflow dispatch event](https://docs.github.com/rest/actions/workflows?apiVersion=2022-11-28#create-a-workflow-dispatch-event) to trigger a workflow run. Each workflow can support a set of inputs by adding a [workflow\_dispatch](https://docs.github.com/actions/using-workflows/workflow-syntax-for-github-actions#onworkflow_dispatch) configuration to the workflow YAML file. [Azure DevOps triggers](https://learn.microsoft.com/en-us/azure/devops/pipelines/build/triggers) are similar and you can also use the Azure DevOps [Pipeline API](https://learn.microsoft.com/en-us/rest/api/azure/devops/pipelines/runs/run-pipeline) for runs. You'll likely see the same capabilities in other products.

![Diagram of example using GitHub Actions as a developer platform provider.](https://learn.microsoft.com/en-us/platform-engineering/media/github-actions-provider.svg)

Diagram of example using GitHub Actions as a developer platform provider.

These workflows or pipelines don't need to be in application source code repositories. The concept would be to take advantage of this fact to do something like this:

- Platform engineers or DevOps team members can maintain the workflows / pipelines in one or more central repositories that developers themselves don't have access to, but the developer platform provider is set up to use. This same repository can include scripts and IaC snippets that the workflows / pipelines use.
- To allow these workflows / pipelines to interact with the appropriate downstream system, ops or other members of your platform engineering team can add the needed secrets in the central repo. See [GitHub Actions](https://docs.github.com/actions/security-guides/encrypted-secrets#about-encrypted-secrets) and [Azure DevOps documentation](https://learn.microsoft.com/en-us/azure/devops/pipelines/process/set-secret-variables) for details on how to do this, or you can opt to centralize the secrets using something like [Azure Key Vault](https://learn.microsoft.com/en-us/azure/key-vault/).
- These workflows / pipelines can then follow a model where they publish any resulting entities as a build / deployment artifact ([GitHub docs](https://docs.github.com/enterprise-cloud@latest/actions/tutorials/store-and-share-data), [Azure DevOps docs](https://learn.microsoft.com/en-us/azure/devops/pipelines/tasks/reference/publish-pipeline-artifact-v1)).
- During a run, the developer platform provider can then watch the state of the workflow/pipeline and update the lifecycle status in the orchestrator until it's complete. For example, you can use web hooks with [GitHub Actions](https://docs.github.com/webhooks/webhook-events-and-payloads#workflow_run) and service hooks with [Azure Pipelines](https://learn.microsoft.com/en-us/azure/devops/service-hooks/events) to track updates.
- Once complete, the provider can then consume the published artifact for inclusion in developer platform graph as needed.

Finally, you can then set up this developer platform provider to output a set of templates into the developer platform graph that reference the appropriate repo and workflow / pipeline, along with inputs for a given task.

The great thing about using a CI/CD system is that they're often set up to support running arbitrary CLIs, so you don’t need a first class, unique integration for everything you do. You can add those over time as needed.

Much of what is described in this example applies to how other types of providers could function. It's also important to note that the use of GitHub Actions or Azure Pipelines in this context doesn't require that you also use them for your actual CI/CD pipelines.

### Other examples

Here are some examples of other types of developer platform providers that could process templates.

| Example | Description |
| --- | --- |
| Source control operations | In some cases, you might need to create or update a repository, submit a PR, or perform another source control-related operation. While general asynchronous workflow engines can manage these kinds of operations, being able to perform basic Git operations without one can be useful. |
| Infrastructure provisioners | While GitHub Actions and Azure Pipelines work well for managing infrastructure provisioning, you can opt for more direct integrations as well. A dedicated provider can streamline setup and avoid overhead. Services like [Azure Deployment Environments](https://learn.microsoft.com/en-us/azure/deployment-environments/overview-what-is-azure-deployment-environments) or [Terraform Cloud](https://developer.hashicorp.com/terraform/cloud-docs) are more directly focused on enabling IaC template-based provisioning and safely and securely. Other examples can include things like creating Kubernetes namespaces for applications in shared clusters or using Git with GitOps workflows using [Flux](https://fluxcd.io/) or [Argo CD](https://argoproj.github.io/cd/) as a specific type of provider. Even more app-centric models like the experimental [Radius](https://radapp.io/) OSS incubation project with their own CLIs could have their own developer platform providers over time. The key thing is to look for and plan for extensibility so you can adapt. |
| Application scaffolding / seeding | Application templates are an important part of where platform engineering leads over time. You can support your template engine of choice by providing a dedicated developer platform provider that is designed to not only scaffold out an application source tree, but also create and push contents into to a source code repository and add the resulting entities into the graph. Every ecosystem has its own application scaffolding preference, whether Yeoman, cookiecutter, or something like the Azure Developer CLI, so the provider model here can allow you to support more than one from your same interfaces. Here again, it’s the extensibility that is key. |
| Manual processes | Whether automatically generating a PR for manual approval or manual workflow steps for nondeveloper personas to respond to using something like Power Platform, the same template-based model can be used in a developer platform provider. You can even move to more automated steps over time. |

While you might not need all these providers to start, you can see how extensibility through something like a developer platform provider can help your automation capabilities grow over time.

### Users and teams

Platform engineering is inherently a multi-system affair, so it’s important to plan how a self-service foundation should handle the more challenging problems with integrating these systems together. Here's a strategy for tackling common challenges with identity, users, and teams.

| Recommendation | Description |
| --- | --- |
| Integrate the developer platform API directly with your identity provider for optimal security. | To secure the developer platform API, we recommend direct integration with an identity provider like [Microsoft Entra ID](https://learn.microsoft.com/en-us/azure/active-directory/), given its robust identity and Entra ID's [RBAC capabilities](https://learn.microsoft.com/en-us/azure/active-directory/develop/howto-implement-rbac-for-apps). There are many advantages to directly using an identity provider’s native SDKs and APIs (for example, via MSAL Entra ID) rather than through an abstraction. You can drive end-to-end security and rely on the same RBAC model throughout while ensuring [conditional access policies](https://learn.microsoft.com/en-us/azure/active-directory/conditional-access/) are continually evaluated (as opposed to only at the time of sign-in). |
| Use single-sign-on and identity provider group integrations in downstream systems. | Your single-sign-on (SSO) integrations should use the same identity provider and tenant that you're using for your developer platform API. Also be sure to take advantage of support any for protocols like [SCIM](https://en.wikipedia.org/wiki/System_for_Cross-domain_Identity_Management) to wire in identity provider groups (like AD groups). Tying these identity provider groups into downstream system permissions isn't always automatic, but at a minimum, you can manually associate identify provider groups with each tool’s grouping concepts without manually managing membership afterwards. For example, you can combine GitHub’s [Enterprise Managed User](https://docs.github.com/enterprise-cloud@latest/admin/identity-and-access-management/using-enterprise-managed-users-for-iam/about-enterprise-managed-users) (EMU) support along with manually taking advantage of the ability to tie [identity provider groups to GitHub teams](https://docs.github.com/enterprise-cloud@latest/admin/identity-and-access-management/using-enterprise-managed-users-for-iam/managing-team-memberships-with-identity-provider-groups). Azure DevOps has [similar capabilities](https://learn.microsoft.com/en-us/azure/devops/organizations/accounts/manage-azure-active-directory-groups). |

### Establish the concept of a team beyond a single identity provider group

As your platform engineering journey continues, you'll likely find that identity provider groups are great for managing membership, but that multiple groups really need to come together to form the concept of a team for RBAC and data aggregation.

In the context of platform engineering, we define a team as a set of people in different roles who work together. For data aggregation, the idea of a multi-role team is critical to power discovery and roll-up information in places like reporting dashboards. On the other hand, a group is a general identity provider concept for a set of users and is designed with the idea of adding multiple people to specific role, rather than the other way around. With RBAC, a team therefore can relate to multiple identity provider groups through differing roles.

![Diagram of multiple identity providers tied to a team.](https://learn.microsoft.com/en-us/platform-engineering/media/team-roles.svg)

Diagram of multiple identity providers tied to a team.

The source of your team data can come from a few different places. For example, if you're using the [teams as code (TAC) pattern](https://learn.microsoft.com/en-us/platform-engineering/engineering-systems#teams-as-code), a developer platform provider can watch for file changes in a repository, and cache them in a user profile and team metadata store. Or you can integrate directly with something like an [Azure Dev Center Project](https://learn.microsoft.com/en-us/azure/deployment-environments/quickstart-create-and-configure-projects) that already has these core RBAC constructs available.

### Establish a model for integrating with downstream systems at the team or user level

While some developer and operations tools/services natively integrate and use identity provider concepts directly, many abstract this into their own representation of a group or user (even with SSO). Beyond enabling access across tools, this reality can also pose problems for data aggregation. Specifically, you might find that APIs in downstream system use their own identifiers rather than identity provider identifiers (for example, the Object ID in Entra ID isn't directly used). That makes filtering and associating user or team level data difficult unless you can map between different IDs.

#### Address team and group level differences

Patterns like [TaC](https://learn.microsoft.com/en-us/platform-engineering/engineering-systems#teams-as-code) can allow you store and access relationships between each system’s team or group identifiers so that you can map between them. To recap, a secure, auditable Git repository becomes the source of a team, and PRs provide a controlled user interface to make updates. CI/CD systems can then update downstream systems and persist the related identifier relationships for the team it used to do so.

![Diagram of teams as code implementation that stores relationships.](https://learn.microsoft.com/en-us/platform-engineering/media/eac-teams-as-code-with-platform.svg)

Diagram of teams as code implementation that stores relationships.

For example, this enables the following relationships to be stored for in API calls:

![Diagram of relationships in API calls with teams as code.](https://learn.microsoft.com/en-us/platform-engineering/media/team-roles-mapped.svg)

Diagram of relationships in API calls with teams as code.

If you would prefer to use a data source other than files in a repository your teams, this same general concept can be applied using the developer platform orchestrator to accomplish the same thing. Under this model, a developer platform provider for the source of the team data can trigger a team update event that all other providers receive and act on as appropriate.

![Diagram of teams as code with Developer Platform.](https://learn.microsoft.com/en-us/platform-engineering/media/teams-via-platform.svg)

Diagram of teams as code with Developer Platform.

### Address user ID challenges

Another related challenge for data access and aggregation is user ID differences. Like in the team case, if you use a system-to-system integration to query data about a user, you can't assume that the identity providers native ID (for example, Object ID for Entra ID) supports a given API. Here again, storing a mapping for a user ID that accesses data through the developer platform API can help. For example, consider GitHub:

![Diagram of user roles with GitHub as a provider.](https://learn.microsoft.com/en-us/platform-engineering/media/user-roles.svg)

Diagram of user roles with GitHub as a provider.

For each system, if you can do a lookup of a user ID in another system via an API without a user token, a given developer platform provider can generate this mapping on the fly. In some cases, this can get complicated since you might need to perform this operation in bulk and cache the results for reference to maintain performance.

### Fall back on using multiple user tokens

For situations where providers need to access user-level data without a way to do user ID translation that would work, the developer platform API can be set up to manage multiple user tokens. For example:

- The developer platform API could support a cache of provider-specific user tokens for use with downstream systems.
- Any interactions with a given provider triggered by the API would include in the provider’s user token if available.
- To handle the case where no user token was available, the provider would trigger an OAuth flow to get one.
- To start, the developer platform API would pass back an authentication URI for an OAuth flow with a redirect URI that was passed into the provider. The URI passed in would include a nonce / one-time-use code.
- The API then returns a *not authenticated* response with the URI.
- Any UX can then use this URI to drive the appropriate authentication flow in a browser.
- Once the redirect happens, the developer platform would receive the needed user token, and cache it for future reference along with the user ID.
- The client could then retry the API call, which would then succeed.

This concept outlines a way to deal with complicated authentication since you can reuse IDs where possible, and don't need to maintain separate redirect URIs per downstream system.

## Use context aware deep links to tools and reporting systems

Up until this point we’ve been talking about the automation aspect of the problem space. This alone can go a long way since your UI can use values in the entities returned during automation to create deep links into other systems for the team.

Even when not automation related, developer platform providers can emit any kind of entity needed. However, you generally don't want to bring all of the detailed data across your entire internal developer platform into your developer platform graph. Dashboards in observability solutions like Grafana, Prometheus, DataDog, or code intelligence in products like SonarQube, and native capabilities in DevOps suites like GitHub and Azure DevOps, are all capable. Instead, the best approach is often to create deep links into these other systems. Your entities can provide sufficient information to create links without directly containing detailed information like log contents.

For cases where you want aggregated and summarized data across tools or need to drive custom metrics, reporting solutions [Power BI](https://powerbi.microsoft.com/) or [Microsoft Fabric](https://www.microsoft.com/microsoft-fabric) can be your next port of call. To merge in team data, you can either connect to your foundation’s database or go through a developer platform API. For example, as described in [Plan and prioritize](https://learn.microsoft.com/en-us/platform-engineering/plan), one place where you might want a custom dashboard is measuring the success of your internal developer platform.

### Be selective with each extra experience you build

While it can be appealing to re-create existing capabilities in something like a common portal, keep in mind you'll also need to maintain it. This is the area where following a product mindset is important. Dashboard-style interfaces are easy to conceive and understand, but your developers might find more value elsewhere.

That said, the model here allows you to use aggregated data in the developer platform graph to create custom user experiences. Entities should have built-in support so they can tie to a user or team. This allows your developer platform API to scope output (along with using indexing and caching).

However, even when you need to create custom UX rather than a deep link, pulling all data into your developer platform graph is typically still not the best approach. For example, consider a situation where you might want to display logs in your UX that already has a well-defined and managed home. Use information in the related entities to help your UX gather information directly from downstream systems.

To start you might need to use a system-to-system integration to connect, but once you’ve implemented one of the models described in [users and teams](#users-and-teams), you can use any stored downstream user/team IDs or user authentication tokens if necessary.

Here are some examples of common experiences to consider:

| Example | Description |
| --- | --- |
| Discovery and exploration | As one platform engineering practitioner put it, "What slows down projects is communication, not developer skills." –Daniel, Cloud Engineer, Fortune 500 Media Company.   Since software is a team sport, creating a user interface to help discover teams, and the entities they own is typically one of the first things to tackle. Cross-team search, discovery, and docs help promote reuse, and aid collaboration for inner sourcing or support. Teams also benefit from having a one stop shop to find things they own including environments, repositories, and other resources like docs. |
| Manual registration of environments or resources | While many things can be provisioned and tracked via the developer platform orchestrator, you might also want to register resources or environments that already exist or aren't automated yet. A simple provider that takes information from a git repository and adds information into resources/environment management can be useful here. If you already have a software catalog, this also becomes a way to integrate it into the model. |
| An API catalog | Tracking APIs that developers should use can go a long way. If you don’t have something already, you can even start with a simple Git repo with a series of files representing APIs, their status, use PRs to manage your approval workflow. These can be added into your developer platform graph so they can be displayed or associated with other entities. For more robust capabilities, you can integrate something like [Microsoft’s API Center](https://learn.microsoft.com/en-us/azure/api-center/set-up-api-center) or another product. |
| License compliance | In some cases, you might also want to provide visibility into software license compliance and license consumption. Developer platforms can also add the automation needed to consume licenses, but even if licenses are assigned manually (for example, via a PR process in a Git repo), developer visibility into what they have (and administrator’s ability to see across everything). |
| An application centric view of Kubernetes | When you use a shared Kubernetes cluster, it can be difficult for developers to find and understand the state of their applications through cluster admin UX. Different organizations might opt to handle this problem differently, but using a namespace to represent an application is one well-known way to do so. From there you can use entities to establish associations between the application’s namespace in the cluster and a team and create a more developer focused view of status for application and provide deep links to other tools or web UIs. |

## User experiences

Different roles in your organization have tools or services that represent a center of gravity for their day-to-day work. The pull of these systems can make it hard for new user experiences outside of these centers of gravity to gain traction. In a perfect world, developers, operations, and other roles can continue to work in an environment that makes sense to them, often those they're already using.

With this in mind, planning for multiple user interfaces as you progress on your platform engineering journey is a good idea. This can also provide an opportunity to start simple, prove value, and grow towards more complex interfaces as the need arises.

### Integrate what you have

If you've read through the [Apply software engineering systems](https://learn.microsoft.com/en-us/platform-engineering/engineering-systems) and [Refine application platform](https://learn.microsoft.com/en-us/platform-engineering/application-platform) articles, you likely identified the systems that you want to continue to use. In either case, evaluate whether you can enhance and extend what you have before you start building new experiences from scratch. (Ask yourself, will people react better to another new user experience or an improved version of something they have now?)

Some of the tools, utilities, or web apps you want to continue using will be custom, and these are good candidates for enhancement. But don't forget to pay attention to whether your favorite tools and services have an extensibility model you can use. You'll get much benefit from starting there. This can eliminate maintenance and security headaches and let you focus on the problem you're trying to solve

For example, you might be able to extend the following surfaces you're already using:

- [Editors](https://code.visualstudio.com/api) and [IDEs](https://learn.microsoft.com/en-us/visualstudio/extensibility/starting-to-develop-visual-studio-extensions)
- Your [DevOps suite](https://learn.microsoft.com/en-us/azure/devops/extend/overview)
- [CLIs](https://docs.github.com/github-cli/github-cli/creating-github-cli-extensions) are increasingly extensible too
- Low/no-code environments like [Power Pages](https://powerpages.microsoft.com/)

![Screenshots of example extensibility for existing systems.](https://learn.microsoft.com/en-us/platform-engineering/media/example-extensibility.svg)

Screenshots of example extensibility for existing systems.

Each might provide a better starting point for a given role than something you set up from scratch since they're existing centers of gravity. Having a common developer platform API as a baseline allows you to swap out things, experiment, and change over time.

#### Consider web editor extensions to create a developer portal

If you're looking for a web-based experience for developers, keep in mind that a recent trend is web-based versions of editors and IDEs. Many, like those that use VS Code, have extension support. With VS Code, anything you build for these web experiences then translates locally for a double benefit.

Beyond services like [GitHub Codespaces](https://github.com/features/codespaces), [vscode.dev](https://vscode.dev/) is a free web version of the VS Code editor with no compute, but includes support for [certain types of extensions](https://code.visualstudio.com/api/extension-guides/web-extensions) including those that use [webviews](https://code.visualstudio.com/api/extension-guides/webview) for custom UI.

![Screenshot of VS Code with an extension using a WebView for custom UX.](https://learn.microsoft.com/en-us/platform-engineering/media/vscode-extensibility.png)

Screenshot of VS Code with an extension using a WebView for custom UX.

Even if your developers don't use VS Code itself, the UX patterns are well known, and can be found in other developer tools. Using vscode.dev can provide a convenient and familiar web-based foundation for developer experiences in addition to the tool itself.

These can act as a developer focused portal in a familiar form that also can translate to local use.

#### ChatOps

Another opportunity that's often overlooked is implementing a ChatOps interface. Given the increase of chat-based interfaces due to rise of AI products like [ChatGPT](https://openai.com/chatgpt) and [GitHub Copilot](https://resources.github.com/copilot-for-business/), [action commands](https://learn.microsoft.com/en-us/microsoftteams/platform/messaging-extensions/how-to/action-commands/define-action-command) or [slash commands](https://api.slack.com/interactivity/slash-commands#:%7E:text=Slash%20Commands%20allow%20users%20to%20invoke%20your%20app,be%20sent%20from%20Slack%20to%20the%20associated%20app.) can provide a useful way to trigger automation workflows, check status, and more. Given most application CI/CD platforms have out-of-box support for systems like [Microsoft Teams](https://github.com/marketplace/microsoft-teams-for-github), [Slack](https://github.com/marketplace/slack-github), or Discord, this can be a natural way to integrate with another user interface developers and related operations roles use every day. Furthermore, all of these products have an extensibility model.

#### Investing in a new developer portal

Assuming you don't have an existing portal or interface you want to use as a base, you might decide to build out a new developer portal. Think about this as a destination rather than a starting point. If you don't already have a development team working with you, starting this effort is the time to do so. Every organization is different, so there's no one-size-fits-all answer for what should be in this kind of experience. As a result, there's no default answer for a prepackaged product that you can spin up and use as-is for something like this today.

For custom-built self-hosted options, general web portal frameworks aren't new, and your development teams might already be using one you could tap into. If you're trying to get out something in front of your users for early feedback, you could even start with something as simple as the low-code [Power Pages](https://powerpages.microsoft.com/) to connect to common developer platform API.

More recent developer portal efforts are more opinionated. For example, [Backstage.io](https://backstage.io/) is a custom developer portal toolkit initially built to meet Spotify’s needs. It includes a CLI to help bootstrap your source tree much like create-react-app does for React.js.

![Screenshot of selecting a component with Backstage.io.](https://learn.microsoft.com/en-us/platform-engineering/media/backstage-component.png)

Screenshot of selecting a component with Backstage.io.

As a portal toolkit, it requires work to get up and customization requires knowledge of TypeScript, Node.js, and React. However, the great thing about it is that, as a toolkit, you can change nearly anything. It does have its own software catalog and templating mechanism as well, but their use isn't required, and it's a well-defined way to bring in new code called plugins.