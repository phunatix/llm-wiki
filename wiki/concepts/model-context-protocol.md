---
title: Model Context Protocol (MCP)
type: concept
source_count: 2
created: 2026-04-10
last_updated: 2026-04-23
tags: [mcp, ai-agents, protocols, governance, interoperability]
inbound_links: 0
status: complete
related_pages: ["[[concepts/agentic-infrastructure]]", "[[concepts/governance-by-default]]", "[[concepts/agentic-development-loop]]", "[[topics/ai-software-development]]", "[[topics/platform-engineering]]"]
---

# Model Context Protocol (MCP)

**Domain**: AI Agent Infrastructure / Interoperability

**One-line definition**: An emerging open standard that lets AI applications discover and use external tools, resources, and services through a uniform server interface — reducing bespoke integrations while introducing a new governance surface for permissions, isolation, and observability.

---

## What MCP Is

The Model Context Protocol defines a standard way for AI clients (models, agents, applications) to connect to MCP servers that expose tools, resources, and prompts. Instead of every AI application building one-off integrations with each external system, MCP creates a common interface: the client discovers what servers are available, what tools they expose, and calls them in a standardized way.

The practical effect: an AI agent can access a filesystem, a database, a web browser, an API, or a custom internal tool through the same protocol — without custom integration code for each target.

---

## Why Governance, Not Just Convenience

The surface appeal of MCP is reducing integration effort. The real operational story is governance.

As MCP adoption grows inside organizations, the registry of available tools becomes an attack surface, a trust problem, and an observability challenge:

- **Permissions**: Which tools can which agents invoke? With what scope?
- **Isolation**: Can a tool invocation by one agent affect another agent's context or state?
- **Provenance**: Who published this MCP server? Is it audited? Is the version pinned?
- **Observability**: Can you trace which agent called which tool, with what arguments, and what it returned?

Treating MCP as just plumbing misses the point. The organizations that get this right will treat MCP servers as governed platform capabilities, not ad hoc scripts.

---

## Registries as Control Plane

One response to the governance challenge: **MCP registries**. A registry provides:
- A catalog of approved MCP servers (versioned, audited, with known publishers)
- Policy controls for tool access (RBAC or attribute-based)
- Runtime visibility into tool invocations

Projects like AgentRegistry OSS represent an early attempt to build this infrastructure. The pattern mirrors what happened with container registries: once Docker made containers easy to create and share, the ecosystem immediately needed Dockerhub, then private registries with scanning and policy. MCP is following a similar arc. (See [[sources/managing-mcp-servers-and-tools-with-agentregistry-oss]])

---

## Standards Context

The Model Context Protocol emerged from Anthropic and has attracted backing from Google, the Linux Foundation, and others — making it a credible candidate for a de facto standard rather than a vendor-proprietary integration layer. The governance of the standard itself (who controls the spec, how extensions are proposed) matters for enterprise adoption decisions. (See [[sources/linux-foundation-google-anthropic-wer-den-standard-fuer-ki-agenten-setzt]])

---

## Key Ideas

- MCP reduces integration burden: one protocol instead of N custom connectors
- The real value is as a governance surface — permissions, isolation, provenance, observability all become tractable
- As agent autonomy increases, MCP registries become as critical as container registries or API gateways
- Organizational MCP adoption without governance is shadow IT by another name

---

## Connection to Platform Engineering

From a platform engineering perspective, MCP servers are a new category of platform capability to expose, govern, and maintain. [[concepts/agentic-infrastructure]] describes the broader shift of AI agents becoming first-class platform actors; MCP is the protocol layer that makes this possible at scale. [[concepts/governance-by-default]] is the design pattern that should govern how MCP tools are exposed.

---

## Open Questions

- Which operational controls are most important to implement first: RBAC, budget caps, audit logging, or environment isolation?
- Will MCP standardize enough to become commodity, or will vendor-specific extensions fragment the ecosystem?
- How does MCP interact with existing API gateway and service mesh infrastructure?

---

## Sources

- [[sources/linux-foundation-google-anthropic-wer-den-standard-fuer-ki-agenten-setzt]] — Strategic context; Linux Foundation + Google + Anthropic backing; governance of the standard
- [[sources/managing-mcp-servers-and-tools-with-agentregistry-oss]] — Registry-oriented governance; AgentRegistry OSS; tool access controls
