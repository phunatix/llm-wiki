# Wiki Evolution Log

**Purpose**: Append-only chronological record of all wiki activity.

Format: `## [YYYY-MM-DD] operation | description`

This helps the LLM understand what's been done recently and is parseable with simple tools.
For example: `grep "^## \[" log.md | tail -10` shows the last 10 entries.

---

## [2026-04-13] init | Wiki structure created

- Created directory structure: `raw/`, `wiki/`, `templates/`
- Initialized CLAUDE.md schema
- Created index.md and log.md
- Ready for first source ingest


---

## [2026-04-13] ingest | Batch ingest of 18 sources from raw/inbox/

**Sources processed**: 18 articles/guides from `raw/inbox/`

**Domains covered**:
- Platform Engineering (3 sources)
- AI & Software Development (4 sources)
- Personal Knowledge Management (3 sources)
- Leadership & Management (4 sources)
- DevOps & Homelab (3 sources + Karpathy pattern)
- Running & Marathon (2 sources)

**Pages created**:

*Topics* (6 new):
- `wiki/topics/platform-engineering`
- `wiki/topics/ai-software-development`
- `wiki/topics/personal-knowledge-management`
- `wiki/topics/leadership-management`
- `wiki/topics/devops-homelab`
- `wiki/topics/running-marathon`

*Entities* (8 new):
- `wiki/entities/Apple`
- `wiki/entities/Eric-J-Ma`
- `wiki/entities/Humanitec`
- `wiki/entities/Kaspar-von-Grunberg`
- `wiki/entities/LM-Studio`
- `wiki/entities/Obsidian`
- `wiki/entities/Proxmox`
- `wiki/entities/Thomas-Dohmke`

*Concepts* (16 new):
- ai-developer-stages, agentic-coding-risks, cognitive-load
- developer-self-service, discretionary-leadership, europe-ai-dependency
- experts-leading-experts, forward-deployed-engineer, functional-organization
- golden-paths, hard-conversations, internal-developer-platform
- llm-wiki-pattern, marathon-interval-training, plain-text-first
- sre-anything-framework

*Summaries* (18 new): One per source

*Analyses* (1 new):
- `wiki/analyses/ai-coding-perspectives-comparison` (Dohmke vs. Zechner synthesis)

**Key insights from this batch**:
- Platform engineering is "10% technical, 90% cultural change" — alignment across all three PE sources
- AI coding agent adoption: deep tension between Dohmke's optimism and Zechner's caution; both credible
- Obsidian + plain text + AI agents = mutually reinforcing choices; Eric J. Ma's system validates this
- Europe's structural AI dependency is a significant geopolitical risk, largely unaddressed
- Apple's functional org (experts leading experts) remains the most counterintuitive and durable org model documented

**Total wiki size after ingest**: 57 pages
