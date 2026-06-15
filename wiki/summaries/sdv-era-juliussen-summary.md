---
title: "Summary: Entering the Software-Defined Vehicle Era (EEtimes)"
type: summary
source_count: 1
created: 2026-06-15
last_updated: 2026-06-15
tags: [summary, software-defined-vehicle, automotive]
source_file: "raw/inbox/Entering the Software-Defined Vehicle Era.md"
related_pages:
  - concepts/software-defined-vehicle
  - topics/software-defined-vehicle
status: complete
---

# Summary: Entering the Software-Defined Vehicle Era

**Source**: EEtimes — "Entering the Software-Defined Vehicle Era"
**Author**: Egil Juliussen (Principal Analyst, VSI Labs; 40 years automotive/high-tech)
**URL**: https://www.eetimes.com/entering-the-software-defined-vehicle-era/
**Published**: 2022-03-21 | **Clipped**: 2026-05-02
**Type**: Industry analysis overview

---

## Key Takeaways

**Scale of complexity**: 100M+ lines of code in many vehicles today; projected to double or triple over the next decade. 50+ ECUs in a high-end 2020 vehicle, each with its own software, connected via CAN bus. CAN bus is being replaced by Ethernet at a growing rate.

**Eight complexity factors unique to automotive**:
1. Product lifetime (10–15 years customer use) × model update cycles (every 3–4 years) × 10–20 models per OEM = enormous maintenance surface
2. Legacy software: All existing systems must be maintained for up to a decade; transition is slow
3. Connected function networks: ECUs form a deeply interconnected web; restructuring is costly
4. Domain ECU transition: Consolidating 50+ ECUs into fewer, more powerful computers — most OEMs "only started a few years ago"
5. Real-time constraints: Engine, braking, steering have hard timing requirements; ADAS/AV especially complex
6. Functional safety: ISO 26262 required for all real-time software; AV safety adds ISO 21448/UL 4600
7. Software legislation: UNECE WP.29 (Europe, 2020) mandates cybersecurity and OTA update management
8. AI: Growing importance for ADAS; "AI black box issues must be solved"

**OEM strategy**: Build vs. buy; growing use of cloud-based development platforms (AWS, Azure as leaders). Low-code/AI-based code generation is an emerging trend. Platform reuse across models and generations is now a competitive priority (was historically low priority).

**BEV opportunity**: Transition from ICE to BEV provides "clean sheet" software opportunity — new BEV models can start with modern, unladen software architecture rather than inheriting legacy ECU software.

---

## Connections

- [[concepts/software-defined-vehicle]] — primary source for complexity factors and OEM phase analysis
