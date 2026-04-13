---
title: "[Guide] The *SIMPLE* Self-Hosted AI Coding That Just Works feat. Qwen3-Coder-Flash"
source: https://www.reddit.com/r/LocalLLaMA/comments/1men28l/guide_the_simple_selfhosted_ai_coding_that_just/
author:
  - "[[xrailgun]]"
published: 2025-08-01
created: 2026-03-18
description:
tags:
  - clippings
  - lmstudio
  - agentic-engineering
---
Hello [r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/), This guide outlines a method to create a fully local AI coding assistant with RAG capabilities. The entire backend runs through LM Studio, which handles model downloading, options, serving, and tool integration, avoiding the need for Docker or separate Python environments. Heavily based on the previous guide by [u/send\_me\_a\_ticket](https://www.reddit.com/user/send_me_a_ticket/) (thanks!), just further simplified.

- I know some of you wizards want to run things directly through CLI and llama.cpp etc, this guide is not for you.

# Core Components

- **Engine:** **LM Studio.** Used for downloading models, serving them via a local API, and running the tool server.
- **Tool Server (RAG):** [**docs-mcp-server**](https://github.com/arabold/docs-mcp-server)**.** Runs as a plugin directly inside LM Studio to scrape and index documentation for the LLM to use.
- **Frontend:** **VS Code +** [**Roo Code**](https://marketplace.visualstudio.com/items?itemName=hitbunt.roo-code)**.** The editor extension that connects to the local model server.

# Advantages of this Approach

- **Straightforward Setup:** Uses the LM Studio GUI for most of the configuration.
- **100% Local & Private:** Code and prompts are not sent to external services.
- **VRAM-Friendly:** Optimized for running quantized GGUF models on consumer hardware.

# Part 1: Configuring LM Studio

**1\. Install LM Studio** Download and install the latest version from the [LM Studio website](https://lmstudio.ai/).

**2\. Download Your Models** In the LM Studio main window (Search tab, magnifying glass icon), search for and download two models:

- **A Coder LLM:** Example: `qwen/qwen3-coder-30b`
- **An Embedding Model:** Example: `Qwen/Qwen3-Embedding-0.6B-GGUF`

**3\. Tune Model Settings** Navigate to the "My Models" tab (folder icon on the left). For both your LLM and your embedding model, you can click on them to tune settings like context length, GPU offload, and enable options like Flash Attention/QV Caching according to your model/hardware.

Qwen3 doesn't seem to like quantized QV Caching, resulting in Exit code: 18446744072635812000, so leave that off/default at f16.

**4\. Configure the** `docs-mcp-server` **Plugin**

- Click the "Chat" tab (yellow chat bubble icon on top left).
- Click on Program on the right.
- Click on Install, select \`Edit mcp.json', and replace its entire contents with this:

    {
      "mcpServers": {
        "docs-mcp-server": {
          "command": "npx",
          "args": \[
            "@arabold/docs-mcp-server@latest"
          \],
          "env": {
            "OPENAI\_API\_KEY": "lmstudio",
            "OPENAI\_API\_BASE": "http://localhost:1234/v1",
            "DOCS\_MCP\_EMBEDDING\_MODEL": "text-embedding-qwen3-embedding-0.6b"
          }
        }
      }
    }

*Note: Your* `DOCS_MCP_EMBEDDING_MODEL` *value must match the API Model Name shown on the Server tab once the model is loaded. If yours is different, you'll need to update it here.*

If it's correct, `the mcp/docs-mcp-server` tab will show things like `Tools`, `scrape_docs`, `search_docs`, ... etc.

**5\. Start the Server**

- Navigate to the Local Server tab (`>_` icon on the left).
- In the top slot, load your coder LLM (e.g., Qwen3-Coder).
- In the second slot, load your embedding model (e.g., Qwen3-Embeddings).
- Click **Start Server**.
- Check the server logs at the bottom to verify that the server is running and the `docs-mcp-server` plugin has loaded correctly.

# Part 2: Configuring VS Code & Roo Code

**1\. Install VS Code and Roo Code** Install [Visual Studio Code](https://code.visualstudio.com/). Then, inside VS Code, go to the Extensions tab and search for and install **Roo Code**.

**2\. Connect Roo Code to LM Studio**

- In VS Code, click the Roo Code icon in the sidebar.
- At the bottom, click the gear icon next to your profile name to open the settings.
- Click **Add Profile**, give it a name (e.g., "LM Studio"), and configure it:
- **LM Provider:** Select `LM Studio`
- **Base URL:** [`http://127.0.0.1:1234`](http://127.0.0.1:1234/) (or your server address)
- **Model:** Select your coder model's ID (e.g., `qwen/qwen3-coder-30b`, it should appear automatically) .
- While in the settings, you can go through the other tabs (like "Auto-Approve") and toggle preferences to fit your workflow.

**3\. Connect Roo Code to the Tool Server** Finally, we have to expose the mcp server to Roo.

- In the Roo Code settings panel, click the 3 horizontal dots (top right), select "MCP Servers" from the drop-down menu.
- Ensure the **"Enable MCP Servers"** checkbox is **ENABLED**.
- Scroll down and click "Edit Global MCP", and replace the contents (if any) with this:

{
  "mcpServers": {
    "docs-mcp-server": {
      "command": "npx",
      "args": \[
        "@arabold/docs-mcp-server@latest"
      \],
      "env": {
        "OPENAI\_API\_KEY": "lmstudio",
        "OPENAI\_API\_BASE": "http://localhost:1234/v1",
        "DOCS\_MCP\_EMBEDDING\_MODEL": "text-embedding-qwen3-embedding-0.6b"
      },
      "alwaysAllow": \[
        "fetch\_url",
        "remove\_docs",
        "scrape\_docs",
        "search\_docs",
        "list\_libraries",
        "find\_version",
        "list\_jobs",
        "get\_job\_info",
        "cancel\_job"
      \],
      "disabled": false
    }
  }
}

*Note: I'm not exactly sure how this part works. This is functional, but maybe contains redundancies. Hopefully someone with more knowledge can optimize this in the comments.*

Then you can toggle it on and see a green circle if there's no issues.

Your setup is now complete. You have a local coding assistant that can use the `docs-mcp-server` to perform RAG against documentation you provide.

---

## Comments

> **Dry-Assistance-367** · [2025-08-01](https://reddit.com/r/LocalLLaMA/comments/1men28l/comment/n6b18jk/) · 15 points
> 
> MCP servers setup in LM Studio only work in the chat window in LM Studio, they do not work in the api server.
> 
> > **xrailgun** · [2025-08-01](https://reddit.com/r/LocalLLaMA/comments/1men28l/comment/n6b2cs5/) · 5 points
> > 
> > Oops... you are right, I've just been running without functionally using it. Turns out it can still work by setting up Roo Code's MCP Servers settings page. Thanks for pointing this out. I'll update the main post.
> > 
> > **modeltrainkarvavado** · [2025-08-02](https://reddit.com/r/LocalLLaMA/comments/1men28l/comment/n6it06z/) · 1 points
> > 
> > I think better use cursor with any mcp you want and serve lm studio model through ngrok and configure it in cursor to make cursor use it
> > 
> > > **bishakhghosh\_** · [2025-08-03](https://reddit.com/r/LocalLLaMA/comments/1men28l/comment/n6qbw8f/) · 1 points
> > > 
> > > Does cursor allow this at all now? Tried with [pinggy.io](http://pinggy.io/) but where to configure the url?

> **prusswan** · [2025-08-01](https://reddit.com/r/LocalLLaMA/comments/1men28l/comment/n6anprd/) · 2 points
> 
> does it matter if you use Roo Code under VS Code or Windsurf?
> 
> > **xrailgun** · [2025-08-01](https://reddit.com/r/LocalLLaMA/comments/1men28l/comment/n6azbky/) · 1 points
> > 
> > sorry I've never heard of Windsurf. it looks great, will play around when I have time.
> > 
> > EDIT: Looks like it's accessing the same VSX marketplace as VS Code, so it *probably* has identical behaviour to the extension in VS Code.

> **Immediate\_Win4776** · [2025-10-19](https://reddit.com/r/LocalLLaMA/comments/1men28l/comment/nkar42d/) · 2 points
> 
> Could someone kindly explain to me the advantages of using embedded models and MCP? It sounds good in theory. But when and how does VSCode > Roo Code use them? It works for me without this additional step, too. Is there an improvement in quality?

> **Danmoreng** · [2025-08-01](https://reddit.com/r/LocalLLaMA/comments/1men28l/comment/n6bk5se/) · 2 points
> 
> I get ~20 T/s in LMStudio vs ~35 T/s with ik\_llama.cpp on my setup.
> 
> > Ryzen 5 7600
> 
> > 32 GB RAM 5600
> 
> > RTx 4070 Ti 12GB
> 
> > **jasonstathame900** · [2025-08-01](https://reddit.com/r/LocalLLaMA/comments/1men28l/comment/n6bpj44/) · 2 points
> > 
> > Which variant of qwen30b coder are you running. I have a similar spec. Vram is 16gb(ti super), 7800x3d. Running 3bit on lmstudio
> > 
> > > **Danmoreng** · [2025-08-01](https://reddit.com/r/LocalLLaMA/comments/1men28l/comment/n6bqoop/) · 5 points
> > > 
> > > IQ4\_XS from here: [https://huggingface.co/unsloth/Qwen3-Coder-30B-A3B-Instruct-1M-GGUF](https://huggingface.co/unsloth/Qwen3-Coder-30B-A3B-Instruct-1M-GGUF)
> > > 
> > > Currently polishing my install script for windows: [https://github.com/Danmoreng/local-qwen3-coder-env](https://github.com/Danmoreng/local-qwen3-coder-env)

> **cantgetthistowork** · [2025-08-01](https://reddit.com/r/LocalLLaMA/comments/1men28l/comment/n6bfpdy/) · 0 points
> 
> docs-mcp-server equivalent for ik\_llama.cpp?

> **prusswan** · [2025-08-01](https://reddit.com/r/LocalLLaMA/comments/1men28l/comment/n6bs118/) · 1 points
> 
> Is there some timeout setting that can be used in case the agent gets stuck? I have seen qwen3 coder keeps adding the same line to a file and needs to be interrupted
> 
> > **xrailgun** · [2025-08-01](https://reddit.com/r/LocalLLaMA/comments/1men28l/comment/n6fqkre/) · 2 points
> > 
> > Is it adding the same line or trying to read the same file repeatedly?
> > 
> > If the former it's probably just model settings like temperature, repeat penalty, etc.
> > 
> > If the latter, something probably went wrong with the mcp server setup, or it wasn't enabled.

> **1Neokortex1** · [2025-08-01](https://reddit.com/r/LocalLLaMA/comments/1men28l/comment/n6c4gnb/) · 1 points
> 
> 🔥🔥🔥 Thank you! I have been researching Cline, and never heard of Roo. I see its a fork version of cline. Does it matter if you use roo or cline with this setup?

> **false79** · [2025-08-01](https://reddit.com/r/LocalLLaMA/comments/1men28l/comment/n6dy4ph/) · 1 points
> 
> I am struggling to get the docs-mcp-server running in Docker Desktop Windows
> 
> I defined:
> 
> DOCS\_MCP\_EMBEDDING\_MODEL="text-embedding-qwen3-embedding-0.6b"  
> OPENAI\_API\_KEY="lmstudio"  
> OPENAI\_API\_BASE="[http://192.168.50.147:1234](http://192.168.50.147:1234/)" # Location of where LM Studio is running qwen3-coder
> 
> in both the .env file as well as passing it through Docker's Run Container's Environmental Variables.
> 
> ❌ Error in main: ConnectionError: Failed to initialize database connection caused by TypeError: Cannot read properties of undefined (reading '0')
> 
> Is there a certain version of
> 
> @arabold/docs-mcp-server
> 
> where this tutorial works?
> 
> > **xrailgun** · [2025-08-01](https://reddit.com/r/LocalLLaMA/comments/1men28l/comment/n6fp9ss/) · 1 points
> > 
> > This tutorial doesn't even touch docker at all. Both mcp jsons are within the LM Studio and VS Code/Roo apps entirely.
> > 
> > > **false79** · [2025-08-01](https://reddit.com/r/LocalLLaMA/comments/1men28l/comment/n6fst8g/) · 2 points
> > > 
> > > ahh thx for steering me into the right direction. I thought I had had to set up the doc-mcp-server as a stand alone service.
> > > 
> > > But now that I look at what the mcp.json is doing in LM Studio, it's using npx command locally to set it up with the env json as arguments.
> > > 
> > > Edit: Woohoo. Uninstall and re-install mcp plugin within LM Studio worked
> > > 
> > > ![Comment Image](https://preview.redd.it/guide-the-simple-self-hosted-ai-coding-that-just-works-feat-v0-ne2in9gswhgf1.png?width=999&format=png&auto=webp&s=416a9704c99551020c1e28567ae37ebf1612d0f2)

> **National-Ad-1314** · [2025-08-01](https://reddit.com/r/LocalLLaMA/comments/1men28l/comment/n6ekfrs/) · 1 points
> 
> Sorry does this require the usual heavy GPU set up?
> 
> > **xrailgun** · [2025-08-01](https://reddit.com/r/LocalLLaMA/comments/1men28l/comment/n6fq8qd/) · 1 points
> > 
> > It depends on the model size and speed you want, and system RAM.
> > 
> > You can run models at slowish speeds entirely on CPU. Anything that runs on LM Studio (llama.cpp backend) should work.

> **Localhost591** · [2025-08-29](https://reddit.com/r/LocalLLaMA/comments/1men28l/comment/nbcvg0k/) · 1 points
> 
> Thank you! This is a perfect use case for LM Studio

> **Localhost591** · [2025-08-29](https://reddit.com/r/LocalLLaMA/comments/1men28l/comment/nbd4u2k/) · 1 points
> 
> Btw remember to download the GGUF not the MLX, if you'd like options for Flash Attention and QV/KV Caching