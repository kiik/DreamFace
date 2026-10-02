# Context ontology and segmentation dimensions

## Aim

Represent an agentic conversation so that its content can be inspected, related, classified, and eventually selected for a bounded context window. Segmentation is not itself a relevance judgment: a segment should remain traceable to its source, and a retention policy should be evaluated separately.

## Layer 0 — the native OpenCode message model

DreamFace does not invent its base categories. Layer 0 is the host system's persisted conversation model, which already provides universal structural segmentation. Category names below come from `@opencode-ai/schema/session-v1` in [anomalyco/opencode](https://github.com/anomalyco/opencode), checked 2026-10-02 on the `dev` branch; they should be re-verified against a pinned release before implementation.

### Messages and roles

- `role` is `user` or `assistant`; an assistant message carries `parentID`, a native responds-to edge pointing at the user message it answers.
- Assistant messages record `agent`, `mode`, `finish` reason, error type, and token/cost accounting; user messages record agent, model, tool visibility, and summary metadata.

### Part types (discriminated union on `type`)

| Part | Native meaning |
| --- | --- |
| `text` | Prose turn content; may be flagged `synthetic` or `ignored`. |
| `reasoning` | Model reasoning trace. |
| `file` | Attachment whose `source` is `file`, `symbol`, or `resource`. |
| `tool` | One tool invocation as a state machine — `pending → running → completed \| error` — with call arguments (`state.input`) and result (`state.output`) in the same part; a completed result records `state.time.compacted` once compaction has cleared its content. |
| `step-start` / `step-finish` | Native step boundaries inside an assistant turn; `step-finish` records a reason, cost, and token delta — a ready-made episode marker. |
| `snapshot` / `patch` | Persisted state snapshots and diffs. |
| `agent` | An agent invocation recorded within a message. |
| `subtask` | Delegation to a subagent, with prompt, description, and agent identity. |
| `retry` | Retry markers. |
| `compaction` | A compaction checkpoint boundary. |

Lifecycle events (`message.*`, `message.part.*`, `session.compacted`, `permission.*`, `todo.updated`, …) define how these entities change over time.

### Why this matters for DreamFace

- Several segmentation decisions are already made for us: message boundaries, roles, tool call/result unification, step boundaries, subagent delegation, and compaction checkpoints.
- DreamFace's linguistic layers (below) are derived annotations over Layer 0, never replacements: every DreamFace segment must be traceable to a native part and span.
- Native hooks align with the console-mode research: `assistant.mode` records a per-turn mode, `subtask` is a Horde-style delegation primitive, and the `compaction` boundary is the native context-management event a DreamFace retention layer must interoperate with.

## Candidate segmentation axes

Treat these as independent axes rather than forcing every segment into one flat taxonomy.

### A. Granularity

Candidate hierarchy, from small to large:

1. token or orthographic unit;
2. word and multiword expression;
3. phrase or clause;
4. sentence;
5. paragraph or list item;
6. section or structured block;
7. message (one speaker turn);
8. exchange (related messages, including tool activity);
9. task episode or session.

Boundaries are language- and format-dependent. Preserve source offsets or equivalent alignment data when splitting text. A segment can have more than one parent when the representation permits cross-cutting structure.

Native alignment: Layer 0 supplies the upper grains — a part is a section/structured block (levels 5–6), a message is level 7, a user message plus the assistant messages referencing it via `parentID` form an exchange (level 8), and a `step-start`…`step-finish` span or a multi-step task is an episode (level 9). Levels 1–4 are DreamFace sub-part segmentation over prose and need explicit spans.

### B. Conversation role and control function

Layer 0 fixes much of this axis: role (`user`/`assistant`), part type, tool state, step boundaries, `subtask` delegation, and lifecycle events. Two refinements remain DreamFace work. First, where Layer 0 unifies a tool call and its result in one `tool` part, derived annotation may split `state.input` (the call) from `state.output` (the result) when their retention needs differ. Second, system/developer instructions arrive as ordinary user-role or synthesized text, so they need a DreamFace control-function label rather than a native role.

### C. Communicative or task function

Candidate labels include goal, constraint, preference, question, plan, commitment, decision, explanation, evidence, observation, result, error, unresolved issue, and social/coordination text. Multi-label annotation may be more faithful than a single exclusive class.

### D. Work-item intent

At the request/work level, distinguish:

- **Delegative:** the desired outcome or responsibility assigned to an agent/person.
- **Procedural:** a method, sequence, policy, or workflow for achieving an outcome.
- **Imperative:** a concrete action that can be carried out or verified.

These labels describe function, not authority. Record speaker, target actor, and source alongside the label; do not infer a mandate solely from grammatical mood.

### E. Relationships

Candidate edges include contains, precedes, responds-to, derived-from, supports, contradicts, refines, blocks, depends-on, duplicates, and belongs-to-work-item. A tree can represent containment and decomposition, while typed edges provide cross-links without forcing the whole conversation into a strict tree.

### F. Lifecycle and epistemic status

Candidate status labels include proposed, accepted, active, completed, superseded, rejected, uncertain, and needs-verification. For factual or experimental claims, record whether the segment is an observation, inference, hypothesis, or decision.

## Candidate segment record

An initial record could contain:

| Field | Meaning |
| --- | --- |
| `id` | Stable identifier within a conversation or corpus item. |
| `span` | Source offsets, message reference, or structured block path. |
| `granularity` | Boundary level from the hierarchy above. |
| `speaker` / `channel` | Origin and conversation role. |
| `type` | Structural function, such as tool call or tool result. |
| `labels` | Zero or more communicative, work-intent, and status labels. |
| `parents` / `relations` | Containment and typed cross-links. |
| `provenance` | Source, timestamp/order, and any transformation history. |
| `language` | Language tag when known; preserve mixed-language spans. |
| `token_cost` | Measured or estimated cost in the target model's tokenizer. |
| `retention` | Candidate include, compress, retrieve-on-demand, or omit decision, with policy/version and rationale. |

A draft wire format exists as [segment.schema.json](../schema/segment.schema.json) (version 0.1, with validating examples in `schema/examples/`); span coordinate units and identifier scope remain open decisions in [RFC 0001](rfcs/0001-context-segments-and-work-item-graphs.md). Avoid storing sensitive payloads in public research corpora; define access, consent, and licensing for each dataset.

## Statistical and Markov-style hypotheses

Markov models may help describe transitions between labelled segments (for example, plan → tool call → result → assistant interpretation), but the memorylessness assumption may discard long-range dependencies that matter to tasks. Compare simple transition models with richer baselines and task-conditioned approaches. Treat predicted transitions as descriptive or decision-support signals until validated; do not use them as sole grounds for deleting context.

## Evaluation principles

- Compare against the unsegmented transcript and straightforward truncation/summarization baselines.
- Measure task outcome and answer grounding as well as token/context cost.
- Track false omission of goals, constraints, tool evidence, and unresolved questions.
- Evaluate calibration and language/task variation; report annotation agreement where human labels are used.
- Make retention decisions reproducible from the policy, model, and evidence version.

See [RFC 0001](rfcs/0001-context-segments-and-work-item-graphs.md) for the initial experiment proposal.
