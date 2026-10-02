# RFC 0001: Context segments and work-item graphs

- **Status:** Draft
- **Authors:** DreamFace project
- **Created:** 2026-10-02
- **Target:** Research framing / prototype design

## Summary

Propose an inspectable representation for agentic chat context using hierarchical segments plus typed cross-links, and a related work-item graph for tracking delegative goals, procedures, and imperative actions. The representation aligns with Layer 0 — the host system's persisted message/part schema (see the [context ontology](../context-ontology.md)) — and treats the research corpus as an [agentic context treebank](../context-treebank.md). This RFC defines a research starting point, not a finalized schema or context-pruning policy.

## Motivation

An agentic context contains more than prose: instructions, requests, assistant plans, tool calls, tool outputs, evidence, and unresolved questions have different functions. A single transcript or a single relevance score may obscure these distinctions. Structured representation could support more transparent context selection and work control.

## Proposal

### Segment layers

Represent source material at multiple available grains: word/expression, phrase/clause, sentence, paragraph/list item, section/block, message, exchange, and episode. Grains at message level and above come from Layer 0 (messages and their `parentID` links, `step-start`/`step-finish` step spans, `subtask` delegation); finer grains are derived sub-part segmentation with explicit spans and source alignment. A message may contain structured parts such as a tool part or a subtask; a tool call and its result are unified in one native `tool` part, and derived annotation may split `state.input` from `state.output` when their retention needs differ.

### Labels and provenance

For each segment, permit separate labels for structural role, communicative/task function, work-item intent, language, lifecycle/epistemic status, and provenance. Labels may be multi-valued and should be versioned. Keep retention policy outputs separate from descriptive labels.

### Work-item graph

Model the initial request as a root with bounded work items. Use containment for decomposition and typed relations for dependency, evidence, response, refinement, conflict, or duplication. Each item should carry an identifier, intent class (delegative, procedural, imperative), desired outcome, actor/owner when known, dependencies, and completion/verification condition.

Use the graph to distinguish deepening (adding constraints or relations to existing items) from widening (adding independent items). Hierarchical sequence labels may aid reference but do not establish execution order; dependencies define ordering.

### Context selection hypothesis

Segmentation and graph relationships may provide features for deciding what to keep, compress, or retrieve. Candidate signals include instruction status, unresolved state, task relation, recency, evidence role, and token cost. Any selection policy must retain provenance and explain its choice. Markov-style transition features are an experimental baseline, not a deletion authority.

## Questions for research

1. Which boundaries and labels can annotators apply reliably across languages?
2. Which segment grains support retrieval and context selection without losing dependencies?
3. Do typed work graphs improve task completion, traceability, or user understanding over a transcript baseline?
4. Which context policies reduce token cost while limiting harmful omissions?
5. How do Plan, Build, Auto, and Horde modes affect success, intervention, and user control?

## Evaluation sketch

Start with a documented synthetic or licensed pilot corpus. Compare the transcript baseline, fixed truncation/summarization, and progressively richer segmentation/selection variants. Include tasks that depend on prior constraints, tool evidence, and unresolved items. Measure task success, evidence/constraint retention, token cost, omission errors, intervention frequency, and annotator agreement. Report per-language and per-task results, not only aggregate scores.

## Open decisions

- Machine-readable serialization and identifier scope.
- Whether span offsets use character, byte, token, or format-native coordinates.
- Which native part types receive DreamFace labels first, and whether a tool part's `state.input` and `state.output` get separate retention decisions.
- Treebank release policy: stable segment IDs, schema versioning, and agreement reporting.
- Core label inventory and adjudication process.
- Corpus languages, collection permissions, and benchmark tasks.
- Integration boundary for OpenCode functions and mode state.
- Retention-policy explainability and reversibility requirements.

## Compatibility and risks

The proposal should be implementable incrementally: source messages remain the record of origin, while segment metadata and links can be added as derived annotations over the Layer 0 schema. Risks include brittle cross-language segmentation, annotation cost, false certainty from labels, graph growth, and policies that remove context based on weak predictions. Preserve the original source and make derived transformations auditable in experiments.

## References

- OpenCode session schema, `@opencode-ai/schema/session-v1` in [anomalyco/opencode](https://github.com/anomalyco/opencode) (`dev` branch, accessed 2026-10-02) — Layer 0 category source; re-verify against a pinned release before implementation.
- Discourse-treebank and dialogue-act literature (RST-DT, PDTB, SWBD-DAMSL, ISO 24617-2, Universal Dependencies) — to be formally cited during the related-work review.
- Any external model or benchmark used should be cited with a version and access date.
