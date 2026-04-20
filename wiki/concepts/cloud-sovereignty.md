---
title: Cloud Sovereignty
type: concept
source_count: 2
created: 2026-04-17
last_updated: 2026-04-17
tags:
  - concept
  - cloud
  - sovereignty
  - geopolitics
  - europe
related_pages:
  - concepts/europe-ai-dependency
  - summaries/forrester-wave-sovereign-cloud-2026-summary
  - summaries/us-cuts-off-tech-to-europe--summary
  - topics/ai-software-development
status: complete
---

# Cloud Sovereignty

## Definition

**Cloud sovereignty** is the ability of an organization or government to maintain control over its data, infrastructure, and operations in the cloud — including where data is stored, who can access it, and under what legal jurisdiction. It encompasses technical, legal, and operational independence from cloud vendors and foreign governments.

Sovereign cloud platforms (SCPs) are the market category that serves this need. They are not plug-and-play solutions — customers use combinations of sovereign architectural options across deployment models and vendors to achieve the level of sovereignty they require.

---

## Deployment Models (Spectrum of Sovereignty)

From most permissive to most restrictive:

| Model | Description | Services Available |
|---|---|---|
| **Public cloud with data boundaries** | Data residency enforced; workloads on hyperscaler infra | Largest set |
| **Sovereign private cloud** | Dedicated infra in-country; vendor operates it | Medium |
| **Air-gapped** | Fully disconnected from internet/vendor networks | Fewest (but growing) |

Trade-off: more sovereignty = fewer available services. Customers must decide how much capability they're willing to sacrifice for control.

---

## Key Concepts

### Data Residency
Data physically stays within defined geographic/legal borders (e.g., EU, Germany, India). Required by many regulations (GDPR, BSI C5, French SecNum Cloud, India DPDPA). Distinct from sovereignty — residency is necessary but not sufficient.

### Operational Sovereignty
The vendor's operations team (who supports, patches, monitors) must also be legally independent of foreign governments. Without this, technical data residency can be undermined by a legal demand on the operating company.

### Legal Insulation
Contracts and corporate structures that prevent foreign courts from compelling data access. Global vendors achieve this via local joint ventures, national partner clouds, or local legal entities staffed by citizens. Examples: Microsoft + Bleu/Delos Cloud, Google + Thales (S3NS), T-Systems + AWS.

### Sovereignty-Washing
The risk that vendors claim sovereign capabilities via superficial features (data residency only) without genuine legal and operational independence. Forrester explicitly flags this: "A cloud platform isn't sovereign simply because it has technical insulation." Customers should interrogate all three layers: technical, operational, and legal.

---

## The EU Context

Cloud sovereignty is acute in Europe because:
- GDPR (2018) established strict data protection requirements
- US CLOUD Act (2018) can compel US companies to hand over data regardless of where it's stored
- European companies increasingly worry about US policy risk (DOGE-era uncertainties, trade policy)
- 70% of European cloud workloads run on US hyperscalers ([[concepts/europe-ai-dependency]])
- EU AI Act and NIS2 Directive increase compliance pressure
- S3NS (Google + Thales joint venture) received France's SecNumCloud certification in December 2025 — the strictest in Europe

Key EU-native options emerging: T-Systems (Germany), STACKIT (Germany/Austria), OVHcloud (France), Aruba (Italy), S3NS (France). None yet matches hyperscaler breadth.

---

## Vendor Landscape (Forrester Wave Q2 2026)

**Leaders** (strongest current offering + strategy):
- **Google Cloud** — Three-tier model (public/private/air-gapped); Gemini/Vertex AI in air-gapped; sovereign as standard feature roadmap
- **Microsoft** — Azure Local, Azure Arc, NACS adoption; sovereign Kubernetes standout; national partner clouds (Bleu, Delos)
- **AWS** — "Control without Compromise"; deep CI/CD sovereign tooling; approach remains fragmented (GovCloud, ESC, Local Zones, AI Factories all separate)
- **Oracle** — Largest range of sovereign options; same price as non-sovereign equivalents (unique in market); niche-focused
- **Tencent Cloud** — Strong for Chinese regulated industries; sovereign private cloud (TCE); language barrier for non-Chinese clients

**Strong Performers**:
- **T-Systems** — Best for DACH (Germany/Austria/Switzerland); Industrial AI Cloud; future open-source stack (VMware alternative)
- **STACKIT** — Germany/Austria data centers; GDPR/BSI C5/ISO 27001; open-source foundations; transparent pricing; limited catalog
- **NxtGen Cloud Technologies** — India-first sovereign cloud; supports Llama 4, DeepSeek R1, Qwen; air-gapped sovereign GitLab/Harbor; limited to India
- **SAP** — SAP-specific sovereign cloud; good for SAP clients; not a general-purpose cloud

**Contenders**: Aruba (Italy), S3NS (France), IBM (financial services), Vultr (affordable global compute), OVHcloud (European infra), Huawei Cloud (China-focused; chips banned in EU/US)

---

## Connection to Europe AI Dependency

Cloud sovereignty is the governance/compliance layer of the same dependency problem documented in [[concepts/europe-ai-dependency]]:
- Structural dependency: Europe runs on US hyperscaler infrastructure
- Legal risk: US law can override European data location
- The sovereign cloud market exists *because* of this dependency — it's the mitigation response
- Same pattern, different angle: European battery dependency (Gigafactory context) → European cloud/compute dependency → European AI compute dependency

All three are expressions of the same underlying problem: strategic technology infrastructure controlled by non-European entities.

---

## Related Pages

- [[concepts/europe-ai-dependency]] — the broader dependency framing
- [[summaries/forrester-wave-sovereign-cloud-2026-summary]] — vendor landscape report
- [[summaries/us-cuts-off-tech-to-europe--summary]] — the geopolitical risk trigger

---

*Sources: Forrester Wave™ Sovereign Cloud Platforms Q2 2026 (2026-04-17); "What If the US Cuts Off Tech to Europe" (2026)*
