---
title: DreamFace research
---

# DreamFace research

DreamFace investigates how to make agentic terminal conversations easier to reason about, control, and evaluate. It pairs research on chat-loop context with prototypes for explicit console functions and modes.

## Research questions

### 1. How should an agentic loop represent its context?

Can a conversation be represented as segments with multiple levels of granularity, semantic function, provenance, and relationships? Which representations help an agent retain useful context while limiting irrelevant or redundant material?

### 2. How should a user control the loop?

What behavior should Plan, Build, Auto, and Horde modes guarantee? Which decisions should be visible, reversible, or subject to user verification?

### 3. How can the ideas be evaluated across languages and tasks?

How do segmentation and selection policies perform across languages, task types, and tool-use patterns? What measures capture task success, retained evidence, context cost, and user control?

## Work areas

- **Context representation:** hierarchical segments, cross-links, provenance, and retention candidates.
- **Loop control:** explicit modes, bounded work items, and observable transitions.
- **Prototype integration:** investigate extension points and constraints in OpenCode before proposing an implementation interface.
- **Agentic context treebank:** multilingual annotated sessions — a shared annotation scheme with per-language releases — with documented provenance, permissions, and agreement reporting.
- **Research outputs:** RFCs, experiment records, and a whitepaper draft.

## Reading map

- [Context ontology](context-ontology.md) describes candidate segmentation axes and metadata.
- [RFC 0001](rfcs/0001-context-segments-and-work-item-graphs.md) proposes an initial representation to test.
- [The agentic context treebank](context-treebank.md) situates corpus work in treebank methodology.
- [Console modes](console-modes.md) describes the four control modes.
- [Languages and terminology](languages-and-terminology.md) describes a path to multilingual research.
- [Whitepaper outline](whitepaper-outline.md) keeps the academic argument and evidence plan visible.

All taxonomies and policies on this site are proposals unless explicitly marked as implemented and evaluated.
