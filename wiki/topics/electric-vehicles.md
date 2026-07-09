---
title: Electric Vehicles & Tesla
type: topic
source_count: 5
created: 2026-04-13
last_updated: 2026-06-22
tags:
  - topic
  - electric-vehicle
  - tesla
  - automotive
  - clean-energy
related_pages:
  - entities/Tesla
  - entities/Tesla-Model-Y
  - entities/Gigafactory-Berlin-Brandenburg
  - concepts/software-defined-vehicle
status: current
---

# Electric Vehicles & Tesla

This topic covers the electric vehicle industry through the lens of Tesla, Inc. — the dominant EV manufacturer from 2020–2025 and the company that defined much of the modern EV playbook.

---

## Entities in This Topic

- [[entities/Tesla]] — Company overview: founding, product timeline, business model, controversies (2003–2026)
- [[entities/Tesla-Model-Y]] — Best-selling car worldwide in 2023; technical specs, variants, safety data
- [[entities/Gigafactory-Berlin-Brandenburg]] — Tesla's European factory; labor, production ramp, site controversies

---

## Key Themes

### From Niche to Mainstream
Tesla's strategy: start premium (Roadster, Model S/X), use profits and learning to build mass-market (Model 3/Y). The Model Y completed this arc by becoming the **world's best-selling car** in 2023 — not just best EV, but best car of any powertrain.

### Manufacturing Innovation
- **Giga Press**: Single-piece rear underbody casting (replaces ~70 parts) — reduces cost, assembly time, structural complexity
- **Octovalve/Super Manifold**: Heat pump system for thermal management across cabin, battery, and motors
- **4680 cells**: Larger cylindrical cells for higher capacity per cell; developed in-house
- **Vertical integration**: Unlike 80%-outsourcing norm in auto, Tesla builds batteries, motors, software in-house

### Sensing Architecture Shift
Radar removed from Model Y/3 in May 2021. Now camera-only (Tesla Vision). Controversial at launch — NHTSA required re-qualification — but Tesla maintained it and FSD continues to build on this approach.

### The Platform Play
NACS (North American Charging Standard) adopted by virtually all US/Canadian EV makers 2023–2024. Tesla's Supercharger network (~7,900 stations, 75,000+ connectors) is now industry infrastructure — a physical platform lock-in analogous to cloud provider lock-in in software.

### Strategic Dependency Mirror
European countries competed intensely for Gigafactory siting because Asia controlled **88% of global battery manufacturing capacity** in 2018. This mirrors the [[concepts/europe-ai-dependency]] pattern: structural dependency on non-European supply chains for strategic technology. Different domain (energy vs. compute), same vulnerability pattern.

### The Musk Variable
By 2025, Elon Musk's political activities had become a material business risk for Tesla: stock declined for 7 consecutive weeks, 200+ global protests in a single day, 29% UK sales decline YoY. Tesla is an unusual case where one person's behavior outside the company creates directly measurable commercial harm — publicly correlated in polling data.

### The Pivot to AI/Robotics (2026)
- Model S and Model X discontinued (Q2 2026) to free capacity for Optimus robot
- Cybercab (robotaxi) targeting production before 2027
- Terafab: Joint Tesla/SpaceX/xAI semiconductor mega-fab for 1 terawatt of AI compute
- Grok chatbot integrated into vehicles; Chinese vehicles allow AI to control vehicle functions

---

## Timeline of Key Milestones

| Year | Event |
|---|---|
| 2008 | First Roadster; first Li-ion production EV |
| 2012 | Model S; first EV to top national monthly sales chart (Norway) |
| 2020 | Model Y launch; enters S&P 500; most valuable automaker |
| 2021 | $1 trillion market cap; Bitcoin investment; Giga Berlin/Texas groundbreaks |
| 2022 | Giga Berlin opens; Cybertruck delayed; Tesla Semi deliveries begin |
| 2023 | Model Y becomes world's best-selling car; NACS adopted industry-wide |
| 2024 | 10% layoffs; Cybercab/Robovan unveiled; IIHS Top Safety Pick+ for Model Y |
| 2025 | Musk political backlash → sales decline; Robotaxi launched Austin; Grok in cars |
| 2026 | BYD overtakes Tesla as world's #1 BEV maker; Model S/X discontinued; Terafab |

---

## The Software-Defined Vehicle Transition

Beyond electrification, the entire automotive industry is undergoing a parallel transformation: the shift to **software-defined vehicles** (SDV). See [[concepts/software-defined-vehicle]] for the full concept page.

Key points connecting to this topic:
- Modern vehicles exceed 100M lines of code across 50+ ECUs; transitioning to domain controllers and eventually central compute
- Tesla is arguably the furthest along this path — camera-only sensing, OTA updates, and FSD are all SDV hallmarks
- BEV platforms provide a "clean sheet" opportunity to build SDV architecture from scratch (vs. retrofitting legacy ICE platforms)
- European research (SofDCar project: Bosch, Mercedes-Benz, KIT, ZF) is developing lifecycle digital twins and security frameworks
- Software maintenance for 10–15 year vehicle lifetimes is an unsolved challenge at industry scale

---

## Open Questions / Areas to Explore

- How does the Chinese EV market (BYD, NIO, Xpeng) compare to Tesla's positioning?
- What is the actual FSD/autonomy status vs. announced timelines?
- How does Optimus robot development intersect with AI agent trends?
- What's the geopolitical impact of NACS becoming the North American standard?
- How do European EV manufacturers (VW, BMW, Stellantis) respond to Tesla's advantage?
- Which OEMs will win the SDV transition — pure-play EVs (Tesla, Rivian) or incumbents with deeper legacy constraints?

---

## Sources (5)

1. [[summaries/tesla-model-y-summary]] — Wikipedia; Model Y vehicle deep-dive
2. [[summaries/gigafactory-berlin-summary]] — Wikipedia; Giga Berlin facility history and controversies
3. [[summaries/tesla-inc-summary]] — Wikipedia; Tesla Inc. company overview (2003–2026)
4. [[summaries/entering-sdv-era--summary]] — Industry overview of SDV complexities; domain ECU transition; OEM strategies (Egil Juliussen, EE Times, 2022)
5. [[summaries/sofdcar-project--summary]] — German research consortium; extended digital twin; lifecycle security (KIT/Bosch, 2021)
