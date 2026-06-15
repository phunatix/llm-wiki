# Wiki Evolution Log

**Purpose**: Append-only chronological record of all wiki activity.

Format: `## [YYYY-MM-DD] operation | description`

This helps the LLM understand what's been done recently and is parseable with simple tools.
For example: `grep "^## \[" log.md | tail -10` shows the last 10 entries.

---

## [2026-04-29] ingest | Batch ingest — 7 articles on AI-assisted development (Thoughtworks + GitHub + cjroth + Heeki Park)

**Sources**:
- `raw/inbox/Assessing internal quality while coding with an agent.md` — Erik Doernenburg, Thoughtworks
- `raw/inbox/Building An Elite AI Engineering Culture In 2026.md` — CJ Roth
- `raw/inbox/Harness engineering for coding agent users.md` — Thoughtworks
- `raw/inbox/Humans and Agents in Software Engineering Loops.md` — Kief Morris, Thoughtworks
- `raw/inbox/Spec-driven development with AI Get started with a new open source toolkit.md` — GitHub
- `raw/inbox/Understanding Spec-Driven-Development Kiro, spec-kit, and Tessl.md` — Birgitta Böckeler, Thoughtworks
- `raw/inbox/Using spec-driven development with Claude Code.md` — Heeki Park

**Skipped** (intentionally out of scope):
- `raw/inbox/Auswandern Als ITler in den USA arbeiten.md` — German IT emigration; personal career topic
- `raw/inbox/Eigenheim vs. ETF Was sich für den langfristigen Vermögensaufbau lohnt.md` — Property vs. ETF investing; personal finance topic

**Created**:
- `[[concepts/harness-engineering]]` — New concept; feedforward guides + feedback sensors; computational vs inferential sensors; three dimensions; humans on/in/outside the loop; agentic flywheel; harness templates
- `[[concepts/spec-driven-development]]` — New concept; three levels (spec-first/anchored/as-source); four-phase workflow; spec-once failure mode; MDD parallel; tool landscape; critical view
- `[[summaries/harness-engineering-for-coding-agents--summary]]`
- `[[summaries/humans-and-agents-software-loops--summary]]`
- `[[summaries/assessing-internal-quality-with-agent--summary]]`
- `[[summaries/building-elite-ai-engineering-culture--summary]]`
- `[[summaries/spec-driven-development-spec-kit--summary]]`
- `[[summaries/understanding-sdd-kiro-spec-kit-tessl--summary]]`
- `[[summaries/using-sdd-with-claude-code--summary]]`

**Updated**:
- `[[concepts/agentic-coding-risks]]` — Added "The Internal Quality Problem" section with Doernenburg's CCMenu case study; source_count 1→2
- `[[topics/ai-software-development]]` — Added harness engineering + SDD to core concepts; 6 new Key Insights (Taste×Discipline×Leverage, AI as mirror, design engineering, AGENTS.md, working code ≠ quality code); 4 new Recent Developments; 8 new Sources by Relevance entries; source_count 5→12

**Key insights added to wiki**:
- Working code ≠ quality code: agents systematically degrade internal quality in ways that compile but accumulate as debt
- Humans on the loop (not in the loop): build the harness that makes agents self-regulate rather than reviewing every line
- The agentic flywheel: agents improving their own harness → self-improving systems
- Taste × Discipline × Leverage: the multiplicative formula for elite AI engineering culture
- Three levels of SDD: spec-first is the practice; spec-anchored is the aspiration; spec-as-source carries real MDD-parallel risks

---

## [2026-04-23] ingest | MCP is eating the world — Stainless (2025-06-21)

**Source**: `raw/inbox/Blog -  MCP is eating the world—and it's here to stay.md`
**Author**: Young-jin Park, Stainless

**Created**:
- `[[summaries/mcp-is-eating-the-world--summary]]`

**Updated**:
- `[[concepts/model-context-protocol]]` (source_count 2→3): added "Why MCP Succeeded Where Others Failed" section with historical predecessors table and four-good-enoughs framework; added adoption flywheel; added "designing at the right altitude" principle; added SDK code mode open question
- `[[topics/ai-software-development]]`: added 2025-06 MCP mainstream adoption to Recent Developments

**Key insights**:
- Four simultaneous "good enoughs" explain MCP's success: models, protocol, tooling, momentum — all crossed the threshold together
- "Designing at the right altitude" — the right abstraction boundary doesn't go away; previous approaches coupled tool definition to specific runtimes
- The adoption flywheel: more tools → better agents → more adoption → models trained on MCP → repeat
- The spec shipped November 2024; adoption exploded February 2025 — timing is distinct from readiness

---

## [2026-04-23] lint | Health check + P1 fixes

**Trigger**: Manual health check request

**Issues found**:
- Two-generation problem: 34 Gen 1 pages (old schema, orphaned, unindexed) coexisted with 77 Gen 2 pages
- Duplicate IDP pages: `concepts/internal-developer-platform.md` (Gen 2) + `concepts/internal-developer-platforms.md` (Gen 1)
- 3 Gen 1 concept pages overlapping Gen 2 equivalents (platform-engineering, site-reliability-engineering, ai-assisted-software-development)
- Index count wrong: said 86, actual was 111
- No broken wikilinks (clean)

**Actions taken — Promoted (Gen 1 → Gen 2 schema)**:
- Created `[[concepts/kubernetes]]` — 8-source page on container orchestration, practical design decisions, cloud-native history
- Created `[[concepts/model-context-protocol]]` — MCP standard; governance framing; registries as control plane
- Created `[[concepts/platform-engineering-maturity-model]]` — CNCF framework; five aspects; four stages; how to use it
- Created `[[concepts/agentic-infrastructure]]` — AI agents as first-class platform actors; agent golden paths
- Created `[[concepts/governance-by-default]]` — Policy-as-code; compliant behavior as default; AI coding scaling implications
- Promoted `[[entities/cncf]]` — CNCF org; Kubernetes steward; maturity model publisher

**Actions taken — Merged and deleted**:
- `concepts/internal-developer-platforms.md` (Gen 1) → unique insights merged into `[[concepts/internal-developer-platform]]`; page deleted
- `concepts/platform-engineering.md` (Gen 1) → role-specialization insight merged into `[[topics/platform-engineering]]`; page deleted
- `concepts/site-reliability-engineering.md` (Gen 1) → SRE-as-discipline section merged into `[[concepts/sre-anything-framework]]`; page deleted
- `concepts/ai-assisted-software-development.md` (Gen 1) → platform-governance insight merged into `[[topics/ai-software-development]]`; page deleted

**Index updated**: Total pages 86 → 92; Concepts 22 → 27; Entities 12 → 13

**Remaining P1 Gen 1 pages (not yet addressed)**:
- `wiki/sources/` (23 pages): Gen 1 source registry; valid files; linked from promoted concept pages; deferred to separate decision
- `wiki/meta/overview.md`: Meta file; not a content page; left as-is
- `wiki/entities/cncf.md`: Promoted above ✅

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

---

## [2026-04-23] ingest | Frugal Architecture (AWS) + Heinzel AI Sysadmin + Kakkar Claude Code Productivity

**Sources processed** (3):
1. "Achieving Frugal Architecture using the AWS Well-Architected Framework guidance" — Ashley DeLoach & Patrick Yurista, AWS Architecture Blog, 2024-08-14
2. "KI-Assistent Heinzel für die Server-Administration im Überblick" — Stefan Wintermeyer, heise.de/iX, 2026-04-15
3. "How I'm Productive with Claude Code" — Neil Kakkar, 2026-03-16

**Pages created** (6):
- `wiki/concepts/frugal-architecture` — Werner Vogels' 7 laws; cost as NFR; frugality = value maximization; Well-Architected Framework mapping table
- `wiki/entities/Heinzel` — AI sysadmin ruleset; architecture diagram; anti-hallucination design; safety prohibitions; three-tier override system; team usage
- `wiki/concepts/agentic-development-loop` — Four friction-removal steps; Theory of Constraints framing; implementer → agent manager identity shift; 5 parallel worktrees
- `wiki/summaries/frugal-architecture-summary` — Key reframe (frugality ≠ cheapness); law-by-law takeaways; connections to cloud-sovereignty and sre-anything-framework
- `wiki/summaries/heinzel-sysadmin-summary` — Architecture, anti-hallucination design, hard safety lines; tool agnosticism; team git workflow
- `wiki/summaries/productive-with-claude-code-summary` — Neil Kakkar's 6 weeks at Tano; Theory of Constraints; threshold effect of build speed; infrastructure over features

**Pages updated** (4):
- `wiki/topics/devops-homelab` — added frugal-architecture concept, Heinzel entity, new summaries; source count 3→5
- `wiki/topics/ai-software-development` — added agentic-development-loop concept, Kakkar summary, March 2026 development entry; source count 4→5
- `wiki/index.md` — 81 pages / 28 sources; added all 6 new pages + new source entries + 1 entity + 2 concepts
- `wiki/log.md` — this entry

**Key insights**:
- Frugal Architecture reframes cost as a *design input* rather than a constraint discovered post-launch; Law 3's security carve-out ("security is never a viable trade-off") is the most practically useful single sentence in the piece
- Heinzel demonstrates that a ruleset-as-system-prompt can enforce safety properties (hard prohibitions, dry-run-first, prompt injection awareness) that would be ignored or forgotten in ad-hoc AI sysadmin work; also shows CLAUDE.md has become a de facto standard project instruction format beyond Anthropic tools
- Kakkar's Theory of Constraints framing is the most useful conceptual lens for the agentic development transition: each friction you remove makes the next constraint visible; the compound effect eventually shifts the developer's highest-leverage work from writing features to building agent infrastructure
- Three sources from this batch naturally form a cluster: Frugal Architecture (cost discipline), Heinzel (AI-in-infrastructure with guardrails), and Kakkar (agentic workflow loops) all address the "how do you operate responsibly at increasing automation levels" question from different angles

**Total wiki size after ingest**: 81 pages / 28 sources

---

## [2026-04-23] ingest | Five Golden Paths articles — major expansion of concepts/golden-paths

**Sources processed** (5):
1. "What are golden paths? A guide to streamlining developer workflows" — Mallory Haigh, platformengineering.org, 2025-01-29
2. "How We Use Golden Paths to Solve Fragmentation in Our Software Ecosystem" — Gary Niemen, Spotify Engineering Blog, ~2020
3. "How to pave golden paths that actually go somewhere" — Aeris Ransom, platformengineering.org, 2023-12-13
4. "Golden Paths: One Size Does Not Fit All" — Bryan Ross, chieftherapyofficer.co.uk, 2025-11-22
5. "Building a golden path to AI" — Matt Asay, InfoWorld, 2025-10-26

**Pages created** (5):
- `wiki/summaries/golden-paths-what-are-they-summary` — Five reasons, vending machine model, value stream mapping design process (Haigh)
- `wiki/summaries/spotify-golden-paths-summary` — Origin story (Dune), rumour-driven development, six success factors, Golden State concept (Niemen)
- `wiki/summaries/golden-paths-day-50-summary` — Day 1 vs Day 2–50; frequency×time prioritization table; DCM as root-cause fix (Ransom/von Grünberg)
- `wiki/summaries/golden-paths-one-size-summary` — Guardrails over gates; 17%→86% adoption case study; composable building blocks (Ross)
- `wiki/summaries/golden-path-to-ai-summary` — AI velocity gap; composable AI guardrails; OpenAI-compatible API standard; data governance layer (Asay)

**Pages updated** (3):
- `wiki/concepts/golden-paths` — Major rewrite: 2 sources → 7 sources; added origin/Spotify, definitions table, Day 1 vs Day 2–50, guardrails over gates, components over completeness, exception handling, DCM, AI golden paths, Golden State, Spotify success factors, prioritization framework
- `wiki/topics/platform-engineering` — Added guardrails/Day 2-50 to key debates; three new key insights; 5 new summaries to sources section; source_count 3→8
- `wiki/index.md` — 86 pages / 33 sources; concept entry updated; 5 new summaries added; 5 new source entries

**Key insights**:
- Golden paths originated at Spotify ~2014 as a Hack Week project named after Dune's "Golden Path" — the term was coined there, not at Humanitec or elsewhere
- The Day 1 vs Day 2–50 insight (von Grünberg) is the most important strategic reframe in this batch: scaffolding is <1% of application lifetime; all the real friction is in ongoing operations. Most platform teams have their priorities exactly backwards.
- Bryan Ross's 17%→86% adoption case study is the most concrete evidence in the wiki for the "standardization through attraction" principle — achieved by reducing mandatory requirements to exactly three non-negotiables and making everything else flexible
- The AI velocity gap (Asay) is the golden paths concept applied to a moving target: monolithic standardization fails precisely because AI models and capabilities evolve faster than committees can approve. The solution (composable APIs + guardrails + exits with obligations) is structurally identical to what Ross recommends for platform engineering generally
- All five sources form a coherent argument: Haigh (what/why) → Spotify (origin/culture) → Ransom/von Grünberg (Day 2-50 prioritization) → Ross (guardrails vs gates) → Asay (AI extension). Reading them in order is a complete education on the topic.

**Total wiki size after ingest**: 86 pages / 33 sources

---

## [2026-06-15] ingest | SPDD + SDV + MCP extensions + Platform Engineering (7 new sources)

**Sources processed** (7 new; earlier session Apr 29 already ingested 7 related articles):
1. "Structured-Prompt-Driven Development (SPDD)" — Wei Zhang & Jessie Jie Xia, Thoughtworks (clipped 2026-05-04)
2. "Entering the Software-Defined Vehicle Era" — Egil Juliussen, EEtimes (clipped 2026-05-02)
3. "Software-Defined Car Foundations for Future Vehicle Generations" — KIT / SofDCar consortium (clipped 2026-05-02)
4. "MCP: An (Accidentally) Universal Plugin System" — Scott Werner, worksonmymachine.ai (clipped 2026-04-10)
5. "I Still Prefer MCP Over Skills" — David, david.coffee (clipped 2026-04-10)
6. "Design a Developer Self-Service Foundation" — juliakm, Microsoft Learn (clipped 2026-06-15)
7. "Build the Platform Engineering Team" — juliakm, Microsoft Learn (clipped 2026-06-15)

**Pages created** (9):
- `wiki/concepts/software-defined-vehicle` — SDV definition; 8 complexity factors; domain ECU transition; OTA; functional safety; OEM software economics; SofDCar
- `wiki/topics/software-defined-vehicle` — New topic area; aggregates SDV entities, concepts, sources
- `wiki/summaries/spdd-structured-prompt-summary` — REASONS Canvas; prompts as first-class team artifacts; fix-prompt-first rule
- `wiki/summaries/sdv-era-juliussen-summary` — 8 SDV complexity factors; domain ECU transition; OEM platform strategy
- `wiki/summaries/sofdcar-kit-summary` — SofDCar consortium; digital twin; IT reference architecture; security methodology
- `wiki/summaries/mcp-universal-plugin-summary` — USB-C analogy; accidental universal plugin ecosystem; protocol evolution
- `wiki/summaries/mcp-vs-skills-summary` — Connectors vs Manuals taxonomy; MCP advantages; ideal MCP+Skill combination
- `wiki/summaries/idp-self-service-foundation-summary` — Five IDP components (API/graph/orchestrator/providers/metadata); automation-first; provider model
- `wiki/summaries/platform-engineering-team-summary` — Reactive vs proactive culture; maturity model; talent gap; Team Topologies

**Pages updated** (4):
- `wiki/concepts/spec-driven-development` — Added SPDD / REASONS Canvas section; source count 3→4
- `wiki/concepts/model-context-protocol` — Added USB-C analogy, accidental network effect, MCP vs Skills taxonomy; source count 2→3
- `wiki/concepts/harness-engineering` — References corrected to existing summary filenames
- `wiki/index.md` — 102 pages / 48 sources; new SDV topic + concept; 8 new summaries listed

**Key insights**:
- SPDD (Structured Prompt-Driven Development) extends SDD by treating prompts as versioned, team-level assets with a formal REASONS Canvas structure. The key rule — "fix the prompt first, then the code" — prevents the common drift between specs and implementation
- The SDV (Software-Defined Vehicle) domain is a major new topic area with unique complexity: 100M+ LOC per vehicle, 10–15 year support lifecycle, real-time safety requirements, and regulatory mandates (UNECE WP.29). The SofDCar project (Bosch + KIT consortium) is the most concrete European research initiative
- MCP's "accidental universality" (Werner's USB-C analogy) is a key architectural insight: MCP was designed for AI context but is becoming a general plugin protocol. The connectors-vs-manuals taxonomy (David's framing) is the clearest mental model for when to use MCP vs Skills
- The Microsoft platform engineering documentation adds the provider/inner-sourcing dimension missing from Humanitec-centric sources: the pluggable provider model is the key to scaling IDP contribution across large organizations without centralizing all maintenance
- Session detected that Apr 29 session had already ingested 8 related articles (Böckeler, GitHub Spec Kit, Heeki Park, Kief Morris, Fowler harness, Doernenburg, Roth elite culture, Stainless MCP); removed 8 duplicate summaries created before discovering this

**Total wiki size after ingest**: 102 pages / 48 sources
