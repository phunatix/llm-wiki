---
title: "Summary: What Are Golden Paths? A Guide to Streamlining Developer Workflows"
type: summary
source_count: 1
created: 2026-04-23
last_updated: 2026-04-23
tags:
  - summary
  - golden-path
  - developer-experience
  - platform-engineering
source_file: "raw/inbox/What are golden paths? A guide to streamlining developer workflows.md"
related_pages:
  - concepts/golden-paths
  - concepts/internal-developer-platform
  - concepts/cognitive-load
  - topics/platform-engineering
status: complete
---

# Summary: What Are Golden Paths?

**Source**: platformengineering.org — "What are golden paths? A guide to streamlining developer workflows"
**Author**: Mallory Haigh (Principal Platform Therapist @ Platform Engineering)
**URL**: https://platformengineering.org/blog/what-are-golden-paths-a-guide-to-streamlining-developer-workflows
**Published**: 2025-01-29 | **Clipped**: 2026-04-23
**Type**: Introductory guide / definitional article

---

## What This Source Contains

A comprehensive introductory guide to golden paths from the Platform Engineering community. Covers definition, the five key benefits, design methodology (including value stream mapping), concrete examples, and the important nuance that golden paths must not become golden cages. Best read as a practitioner's foundation document.

---

## Key Takeaways

### The Definition
> "A golden path is a preconfigured, paved road that provides an end-to-end workflow for developers. It's a predefined route that guides developers through common tasks, designed to reduce cognitive load and ensure that they can operate safely and in compliance."

The "happy path" equivalent in software engineering, but for platform/infrastructure workflows rather than code execution paths.

### Five Reasons Golden Paths Matter
1. **Reduced cognitive load** — frees developers from infrastructure/security complexity
2. **Improved consistency and reliability** — uniform processes reduce errors and simplify troubleshooting
3. **Faster development cycles** — self-service eliminates approval wait times
4. **Enhanced security and compliance** — best practices baked in, not bolted on
5. **Developer satisfaction** — less frustration, more engagement

### The "Vending Machine" Mental Model
Platform engineering = operating a vending machine. Platform engineers stock the machine; developers select what they need and receive a uniformly delivered product. This framing clarifies the interface design challenge: the product must be recognizable, accessible, and reliably delivered — not a bespoke interaction every time.

### Design Process
Value stream mapping first: visualize steps, lead times, process times, and completion rates before designing any path. This prevents building golden paths for problems that aren't bottlenecks. Prioritize by frequency × impact. Build iteratively from a Minimum Viable Platform.

### The Golden Path ≠ Golden Cage
Golden paths should be escapable. When developers go off-path, the platform should make that visible — new requirements discovered off-path become candidates for standardization. The path should attract, not cage.

---

## Connections to Existing Wiki

- **[[concepts/golden-paths]]** — this article provides the foundational definitional layer; its 5-reason framework is integrated into the concept page
- **[[concepts/cognitive-load]]** — cognitive load reduction is explicitly cited as the primary purpose
- **[[concepts/developer-self-service]]** — self-service capabilities are the delivery mechanism for the path
