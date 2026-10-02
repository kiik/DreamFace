# DreamFace

**DreamFace** is a research and prototyping project about controllable agentic chat loops and extending the OpenCode terminal experience with explicit, inspectable functions.

The project is being developed as MSc computer-engineering lab material. Research notes, RFCs, and whitepaper drafts live beside prototypes so that hypotheses, terminology, implementation decisions, and evaluation can evolve together.

## Research tracks

1. **Agentic chat-loop control** — model conversation context as structured, bounded work and evidence rather than an undifferentiated transcript. Investigate segmentation, context selection, compression, and control policies.
2. **A custom agentic console experience** — explore how explicit functions and control modes can extend OpenCode workflows while remaining inspectable and user-steerable.

## Console modes under study

| Mode | Intended behavior |
| --- | --- |
| **Plan** | Dry prework: inspect the request, produce a bounded plan and expected changes, and make no project mutations. |
| **Build** | Work in increments with user verification at defined checkpoints. |
| **Auto** | Execute the agreed scope without routine checkpoints, reporting decisions and results. |
| **Horde** | Decompose work into a tree of bounded work items and coordinate multiple agents where parallel work is useful. |

These are research definitions, not yet implemented guarantees. See [the mode proposal](docs/console-modes.md).

## Start here

- [Project overview and research agenda](docs/index.md)
- [Context ontology and segmentation dimensions](docs/context-ontology.md)
- [RFC 0001: Context segments and work-item graphs](docs/rfcs/0001-context-segments-and-work-item-graphs.md)
- [The agentic context treebank](docs/context-treebank.md)
- [Console modes](docs/console-modes.md)
- [Multilingual corpus and terminology plan](docs/languages-and-terminology.md)
- [Whitepaper outline](docs/whitepaper-outline.md)
- [RFC process](docs/rfcs/0000-rfc-process.md)
- Machine-readable artifacts: [segment schema](schema/segment.schema.json), [work-item schema](schema/work-item.schema.json), [terminology register](terminology/concepts.yml)
- [RFC template](docs/rfcs/rfc-template.md)

## Status

This repository is at the research-framing stage. Proposed taxonomies and policies are hypotheses to refine through RFCs, prototype experiments, and documented evaluation. No OpenCode integration or context-pruning behavior is claimed to exist yet.

## Contributing and citation

Use GitHub issues for bounded questions and experiments, and RFCs for changes to shared concepts or interfaces (see the [RFC process](docs/rfcs/0000-rfc-process.md)). Research claims should identify their evidence and limitations. Cite DreamFace via `CITATION.cff` (GitHub renders BibTeX/APA from it).

## License

Research materials — documentation, RFCs, schemas, terminology, and corpora — are licensed [CC BY 4.0](LICENSE). Current and future code is MIT-licensed under [LICENSE-CODE](LICENSE-CODE). Corpus releases may add access terms where sessions contain non-synthetic, consented data.
