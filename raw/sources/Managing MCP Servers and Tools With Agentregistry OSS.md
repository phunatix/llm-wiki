---
title: Managing MCP Servers and Tools With Agentregistry OSS
source: https://dev.to/thenjdevopsguy/managing-mcp-servers-and-tools-with-agentregistry-oss-4iga
author:
published: 2026-04-05
created: 2026-04-10
description: In Platform Engineering, the whole goal, at a high level, is to make software delivery and... Tagged with kubernetes, programming, devops, docker.
tags:
  - clippings
---
Three big topics when it comes to MCP:

1. How do you know the MCP Server is secure?
2. Where is it stored?
3. Is it version-controlled, or can anyone just change it at any time?

And that's where having an MCP registry comes into play.

In this blog post, you'll learn how to securely store your MCP Server, and it's available tools to be used later within your Agents.

## Quick Recap: What Is MCP?

Model Context Protocol (MCP) is a spec/standard created by and open-sourced Anthropic. The goal of MCP is to have a server that hosts tools, and these tools are able to implement certain functionality for what you're working on. For example, you can use a Kubernetes MCP Server that can do everything from list/describe/log Pods and deploy objects to Kubernetes. MCP uses JSON-RPC 2.0 for it's communication layer underneath the hood for communication between an Agent (the client) and MCP tools (hosted on the server).

### The "Is MCP Dead" Debate

I was at MCPDevSummit in NY this week, and I caught a keynote that explained the need for MCP Server tools pretty nicely from a theoretical perspective. Right now, it may be easier for Agents to talk to MCP Server tools vs having them talk tens or hundreds of APIs directly. The reason why is that it's simpler for an Agent to call a tool and have that tool (because a tool, underneath the hood, is simply a function/method) call the APIs instead. What this could come down to is less tokens used and less context bloat, along with hopefully, better results.

## Configuring Agentregistry Locally

With an understanding of what MCP is at a high level, let's dive into the hands-on portion of this blog post. In this section, you'll get agentregistry deployed, which takes around 30 seconds.

1. Pull down the latest version of agentregistry.
```
curl -fsSL https://raw.githubusercontent.com/agentregistry-dev/agentregistry/main/scripts/get-arctl | bash
```
1. Run the following command, which starts the agentregistry daemon.
```
arctl daemon start
```

You'll see an output similar to the following:  

```
Starting agentregistry daemon...
✓ agentregistry daemon started successfully
```
1. Open Docker and you'll see agentregistry running along with a link you can click to reach the UI.

[![ ](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F2o2r4btqcxw1leuo18b4.png)](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F2o2r4btqcxw1leuo18b4.png)

You should now see the agentregistry UI.

[![ ](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F9ovggf398k1qhfgzwqrt.png)](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F9ovggf398k1qhfgzwqrt.png)

Sidenote: if you have a remote registry, you can connect to it with the following:  

```
arctl --registry-url http://YOUR-HOST:12121 version
```

## Adding An MCP Server To Agentregistry

With agentregistry deployed, you can now add an MCP Server to the registry to ensure it's stored and secured. For testing purposes, lets use the filesystem MCP Server that's stored on GitHub.

1. Using `arctl mcp publish`, you'll pass in the following flags.
2. 1. MCP Server: server-filesystem
		2. Type: NPM
		3. Version: 0.6.3
```
arctl mcp publish io.github.modelcontextprotocol/server-filesystem --type npm --package-id
  @modelcontextprotocol/server-filesystem --version 0.6.3 --description 'MCP server for filesystem access' --git
  https://github.com/modelcontextprotocol/servers.git -v
```

The MCP Server will now show in your registry.

[![ ](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F0le5e7xcxkaqqwd8dw67.png)](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F0le5e7xcxkaqqwd8dw67.png)  
[![ ](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fxe8777eysnt9hbrekdq5.png)](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fxe8777eysnt9hbrekdq5.png)

You can also add your MCP Server via the UI.

1. Click the purple **\+ Add** button and choose **Server**.

[![ ](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fvrco0sa7biqz3v7cip0d.png)](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fvrco0sa7biqz3v7cip0d.png)

1. Add in the details about your MCP Server.

[![ ](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fuiax24owam8a047oxluc.png)](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fuiax24owam8a047oxluc.png)

## Conclusion

Having a safe, secure, and reliable place to store something as prone to security incidents as MCP Servers is key to creating a proper posture for you and your organization when using AI. This is why agentregistry can also be used to store Agent Skills and prompts. Because the majority of what you're using is either a function/method (an MCP Server tool) or.MD files/text files, shadow AI can easily occur.[MongoDB](https://dev.to/mongodb)Promoted

[![Gen AI apps are built with MongoDB Atlas](https://media2.dev.to/dynamic/image/width=775%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fi.imgur.com%2FlGiI0TQ.png)](https://www.mongodb.com/cloud/atlas/lp/try3?utm_campaign=display_devto-programming_pl_flighted_atlas_tryatlaslp_prosp_gic-null_ww-all_dev_dv-all_eng_leadgen&utm_source=devto&utm_medium=display&utm_content=airevolution-v1&bb=238218)

## Gen AI apps are built with MongoDB Atlas

MongoDB Atlas is the developer-friendly database for building, scaling, and running gen AI & LLM apps—no separate vector DB needed. Enjoy native vector search, 115+ regions, and flexible document modeling. Build AI faster, all in one place.