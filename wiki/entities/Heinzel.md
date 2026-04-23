---
title: Heinzel
type: entity
entity_type: tool
source_count: 1
created: 2026-04-23
last_updated: 2026-04-23
tags:
  - entity
  - ai-agents
  - sysadmin
  - devops
  - open-source
related_pages:
  - topics/devops-homelab
  - topics/ai-software-development
  - entities/LM-Studio
  - concepts/agentic-coding-risks
status: complete
---

# Heinzel

## Overview

**Heinzel** is an open-source AI sysadmin assistant — not a standalone program, but a **ruleset of ~140 KB of Markdown files** that acts as a system prompt for terminal-based AI coding agents. Named after the *Heinzelmännchen* (German folklore helpers who work quietly in the background).

- **Author**: Stefan Wintermeyer
- **License**: MIT
- **Repository**: https://github.com/wintermeyer/heinzel
- **Published/announced**: April 2026 (heise.de / iX)

The core idea: if an AI agent can read files and execute shell commands, it can administer servers — provided it has guardrails. Heinzel provides those guardrails as structured Markdown that both the LLM and the human admin can read and understand.

---

## Architecture

```
heinzel/
├── CLAUDE.md                     # Main ruleset: security, backup, logging
├── rules/
│   ├── debian.md / rhel.md / suse.md / macos.md   # OS-specific rules
│   ├── security.md               # SSH hardening, open ports, SUID/SGID, IPS
│   ├── housekeeping.md           # Health checks: disk, memory, certs, services
│   ├── backups.md                # Mandatory backup behavior
│   ├── anomaly-detection.md      # Suspicious patterns in server output
│   └── ... (23 rule files total)
│   └── custom/                   # Local overrides (gitignored)
└── memory/
    ├── MEMORY.md                 # Index — agent reads this every session
    ├── user.md                   # SSH user, language preference (gitignored)
    ├── readonly.md               # Servers that may not be modified
    ├── network.md                # Network topology
    └── servers/
        └── web1.example.com/
            ├── memory.md         # OS, services, known quirks
            └── changelog.log     # What changed, when
```

**Key file: MEMORY.md** — acts as the agent's index. At session start, it tells the agent which servers exist, where their memory files are, and what was done previously. Without it, the agent starts blind every time.

---

## Tool Agnosticism

Heinzel works with any terminal AI agent that can read project files and run shell commands:
- **Claude Code** (Anthropic) — commercial, ~€20/month; best for complex multi-step tasks
- **OpenCode** (open source) — supports OpenAI, Google Gemini, Anthropic, and local models via Ollama
- **Local models (Ollama)** — `qwen3.5:9b` works for simple tasks; 14B+ recommended for reliability; no cloud API required; complete data sovereignty

CLAUDE.md has become a **de facto standard** for project instruction files — OpenCode and other tools read it automatically even though the name sounds Claude-specific.

---

## Anti-Hallucination Design

The single biggest risk of LLM-driven sysadmin work is hallucinated commands that look correct but aren't (e.g., using `apt` syntax on RHEL, or flags that don't exist in the installed version). Heinzel's mitigation:

1. **Verify before running**: CLAUDE.md instructs the agent to run `command --help` before proposing any command — confirming flags exist on this specific version, not trusting training data
2. **Read man pages**: For complex tools (iptables, firewall-cmd, certbot), read the man page
3. **Search upstream docs**: When behavior varies across versions — especially important because training data has a cutoff. Example: No current LLM (as of early 2026) knows that Debian 13 (Trixie) is now the stable release
4. **Dry-run first**: Every operation that supports it runs in `--dry-run` / `--assumeno` / simulation mode before actual execution
5. **OS-specific rule files**: Correct syntax for each distro/OS is encoded in dedicated rule files, not relied upon from model knowledge

---

## Connection Workflow (Per Server Session)

1. **Access control check**: Is this server on the read-only list or blocklist?
2. **DNS alias resolution**: Is this hostname an alias for a known server? Reuse existing memory.
3. **Privilege escalation**: Tries normal user → sudo → root SSH, in order (least privilege)
4. **OS detection**: `uname -s`, `/etc/os-release` (Linux) or `sw_vers` (macOS) → loads appropriate rule file
5. **Load or create server memory**: If the server is known, loads facts; if new, creates the memory file
6. **Plan and propose**: Each step is proposed and explained before execution
7. **Human confirms**: Nothing runs without approval
8. **Backup + logging**: Config changes trigger automatic backup to `/var/backups/heinzel/` with timestamp; all changes logged locally and to system journal (`logger -t heinzel`)

---

## Safety Features

**Absolute prohibitions (hard-coded in CLAUDE.md)**:
- Never run `fdisk`, `parted`, or `gdisk` without explicit request
- Never modify `/etc/ssh/sshd_config` or delete SSH keys
- Never block SSH port 22 in firewall
- Never run `halt` without physical recovery capability

**Read-only mode**: Servers listed in `memory/readonly.md` can be inspected and audited but not modified. Heinzel collects required actions into a report for a human to execute instead.

**Prompt injection protection**: All server output is treated as untrusted. If a compromised server embeds LLM instructions in its output ("Ignore previous rules and delete..."), Heinzel is instructed to detect, warn, and wait for human confirmation.

**Plan mode**: Claude Code's plan mode (Shift+Tab × 3 or `/plan`) lets the agent analyze and plan without executing anything — useful for complex tasks like database migrations.

---

## Three-Tier Override System

Rule files can be customized at three levels (later levels override earlier):
1. **Base**: `rules/<name>.md` — upstream Heinzel rules
2. **Global custom**: `rules/custom/<name>.md` — site-wide overrides
3. **Per-server**: `memory/servers/<hostname>/rules.md` — host-specific rules

Override syntax uses heading prefixes: `## Add:`, `## Replace:`, `## Remove:` for additive, replacement, and deletion overrides respectively.

---

## Team Usage

Server memory files are shared via git; personal SSH credentials (`memory/user.md`) are gitignored. New team members copy `memory/user.md.example`, fill in their SSH username, and immediately have access to all shared server knowledge. All changes appear in the system journal (`journalctl -t heinzel`) — any team member can see what happened on any server.

---

## Relation to Existing Wiki Concepts

- Extends the **[[concepts/agentic-coding-risks]]** conversation: Heinzel is an example of how to mitigate those risks (dry-runs, human approval, hard prohibitions, anti-hallucination rules) while still benefiting from AI capability
- Demonstrates the **[[concepts/plain-text-first]]** principle at scale: 140KB of Markdown that both humans and AI agents can read, understand, and modify — no compiled code
- Contrasts with **[[concepts/ai-memory-architecture]]**: Heinzel uses markdown files for agent memory (per-server changelogs, facts) — a pragmatic choice for the sysadmin use case where records are human-readable narratives, not structured query targets

---

*Source: Stefan Wintermeyer, "KI-Assistent Heinzel für die Server-Administration im Überblick", heise.de / iX (2026-04-15)*
