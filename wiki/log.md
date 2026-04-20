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

---

## [2026-04-13] ingest | Tesla Model Y (Wikipedia)

**Source**: `raw/inbox/Tesla Model Y.md` — Wikipedia article, 105 KB, clipped 2026-04-13
**Domain**: Automotive / Electric Vehicles (new domain — first non-tech/running source)

**Pages created** (2):
- `wiki/entities/Tesla-Model-Y` — structured entity page with specs, variants, safety ratings, sales data, market breakdown
- `wiki/summaries/tesla-model-y-summary` — source summary with key takeaways and connections

**Key facts extracted**:
- Model Y became the world's best-selling car (all powertrains) in 2023 — 1,211,601 units
- 2025 Juniper refresh: full-width lightbar, 15.4" screen, Standard trim added Oct 2025
- Model Y L: 6-seat long-wheelbase launched China Sept 2025; AU/NZ first export market Mar 2026
- Giga Press: single-piece rear underbody casting replaces ~70 stamped parts (manufacturing innovation)
- Octovalve/Super Manifold heat pump: significant cold-weather range advantage
- Vision-only sensing (no radar) since May 2021
- Hidden door handle controversy: China mandating design change by Jan 1, 2027; NHTSA investigating 174K+ vehicles
- Safety: NHTSA 5-star, Euro NCAP 5-star (97% adult 2022), IIHS Top Safety Pick+ 2024
- India launch July 2025; first Chinese government procurement eligibility June 2024

**Domain note**: This source stands alone — no strong connections to existing wiki clusters (platform engineering, AI coding, PKM, leadership, homelab, running). Represents an isolated domain expansion. If more EV/automotive sources are ingested, consider creating `topics/electric-vehicles`.

**Total wiki size after ingest**: 59 pages / 19 sources

---

## [2026-04-16] ingest | Gigafactory Berlin-Brandenburg + Tesla, Inc. (Wikipedia)

**Sources**:
- `raw/inbox/Gigafactory Berlin-Brandenburg.md` — Wikipedia, 84 KB, clipped 2026-04-16
- `raw/inbox/Tesla, Inc..md` — Wikipedia, 370 KB (largest source in wiki), clipped 2026-04-16

**Domain**: Electric Vehicles / Tesla (expanding the EV cluster started with Tesla Model Y)

**Pages created** (6):
- `wiki/entities/Gigafactory-Berlin-Brandenburg` — site history, production ramp, labor relations, incidents, opposition
- `wiki/entities/Tesla` — company overview: founding, product timeline, Gigafactory network, energy business, tech, controversies
- `wiki/summaries/gigafactory-berlin-summary` — source summary with cross-links to europe-ai-dependency pattern
- `wiki/summaries/tesla-inc-summary` — source summary highlighting Musk political risk, robotics pivot, FSD shift, NACS win
- `wiki/topics/electric-vehicles` — new topic page aggregating all 3 Tesla sources with key themes and open questions

**Key insights**:
- Tesla lost the world's largest BEV manufacturer title to BYD in January 2026 — quietly significant given 5 years of dominance
- Tesla is pivoting from premium sedan/SUV to robotics (Optimus) and AI (Terafab with SpaceX/xAI) — Model S/X discontinued Q2 2026
- Elon Musk's political activities became a material, quantified business risk in 2025: 7 weeks of stock decline, 200+ simultaneous protests, -29% UK sales
- NACS as industry standard is a rare physical infrastructure lock-in play — analogous to cloud platform capture
- Giga Berlin labor issues (30% sickness rate, IG Metall campaigns, arson) contrast sharply with Tesla's product reputation
- European battery dependency (88% Asian production in 2018) mirrors the AI dependency pattern already in the wiki — same structural vulnerability, different domain
- Giga Berlin still hasn't hit 250K/year target (half capacity) as of August 2025 — production ambition vs. reality gap

**Cross-links created**:
- `europe-ai-dependency` ↔ Giga Berlin site selection context (battery dependency as strategic vulnerability)
- `Tesla-Model-Y` ↔ `Tesla` ↔ `Gigafactory-Berlin-Brandenburg` (three-way entity cluster)

**Total wiki size after ingest**: 65 pages / 21 sources

---

## [2026-04-16] ingest | Two opinionated approaches to PKM — Crystal Lee

**Source**: `raw/inbox/Two opinionated approaches to personal knowledgement management — Crystal Lee (she她).md`
**URL**: https://crystaljjlee.com/blog/two-approaches-to-pkm/
**Published**: 2024-05-16 | **Clipped**: 2026-04-16
**Domain**: Personal Knowledge Management (deepening existing cluster)

**Pages created** (3):
- `wiki/concepts/para-method` — PARA (Projects/Areas/Resources/Archive); Tiago Forte; discoverability-first; relation to LLM Wiki
- `wiki/concepts/johnny-decimal` — JD numeric addressing; searchability-first; static hierarchy; JD Index as reference notes
- `wiki/summaries/two-pkm-approaches-summary` — source summary

**Pages updated** (1):
- `wiki/topics/personal-knowledge-management` — added PARA and JD to Core Concepts; updated source count 3→4

**Key insight**: The searchability vs. discoverability framing is the sharpest distillation of why different PKM systems appeal to different people — and why Zettelkasten/wikilinks/LLM Wiki approaches outperform flat hierarchies for knowledge (as opposed to files). The LLM Wiki pattern is effectively an AI-maintained Zettelkasten: linked, designed for rediscovery, not static archiving.

**Total wiki size after ingest**: 68 pages / 22 sources

---

## [2026-04-17] ingest | Forrester Wave Sovereign Cloud + Edwards PKM critique + MindStudio tutorial

**Sources** (3):
- `raw/inbox/The Forrester Wave™ Sovereign Cloud Platforms, Q2 2026.md` — Forrester analyst report, 39 KB, clipped 2026-04-17
- `raw/inbox/Stop Calling It Memory The Problem with Every "AI + Obsidian" Tutorial.md` — Substack essay (Jonathan Edwards), 26 KB, clipped 2026-04-16
- `raw/inbox/How to Build an AI Second Brain with Claude Code and Obsidian.md` — MindStudio blog tutorial, 17 KB, clipped 2026-04-16

**Pages created** (7):
- `wiki/concepts/cloud-sovereignty` — sovereign cloud definition, deployment models, sovereignty-washing, EU context, vendor landscape map
- `wiki/concepts/ai-memory-architecture` — the markdown-vs-database debate for AI agent knowledge; when each is appropriate; reconciliation
- `wiki/summaries/forrester-wave-sovereign-cloud-2026-summary` — 12 vendor evaluations, key findings, EU implications
- `wiki/summaries/stop-calling-it-memory-summary` — Edwards' critique, five failure modes, his SQLite+Kuzu production system
- `wiki/summaries/mindstudio-ai-second-brain-summary` — practical Claude Code+Obsidian workflows; the "other side" of the debate

**Pages updated** (1):
- `wiki/topics/personal-knowledge-management` — added ai-memory-architecture concept, new debate entry, 3 new summaries, source count 4→6

**Key insights**:
- Sovereign cloud is the governance/compliance layer of the same structural dependency as `europe-ai-dependency` — the cure (US hyperscaler sovereign offerings) still involves dependency on US companies, just with legal/structural insulation
- The Edwards/MindStudio sources represent opposite sides of the same debate (markdown-first vs. database-first for AI memory) — both are now in the wiki with a reconciling concept page; this wiki uses markdown-first deliberately for knowledge articles, not structured operational records
- Sovereignty-washing is the sovereign cloud equivalent of greenwashing — technical data residency without legal/operational independence is insufficient
- Three independent structural dependency patterns now documented in the wiki: battery manufacturing (88% Asian), cloud/AI compute (70% US), sovereign cloud (US hyperscalers lead the "sovereign" market too)
- Google Cloud's air-gapped AI (Gemini/Vertex in fully disconnected environment) is a genuine differentiator no competitor has matched
- OVHcloud faces a real legal paradox: Canada ordered it to provide access to data stored in France — compliance violates French law, non-compliance risks contempt charges

**Total wiki size after ingest**: 75 pages / 25 sources
