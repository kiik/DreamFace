# The agentic context treebank

## Is DreamFace building a treebank?

Yes — the closest description of the corpus work is a treebank, with two twists: the "text" is a multi-party agentic session, and the annotation serves an operational goal (context selection and loop control) in addition to linguistic study.

Classical treebank construction: take raw text, fix a segmentation (tokenization, sentence boundaries), annotate hierarchical structure over the segments (constituency or dependency trees), add functional layers (function tags, semantic roles, discourse relations), and publish with annotation guidelines, inter-annotator agreement statistics, and versioned releases. The Penn Treebank and Universal Dependencies did this for syntax; the RST Discourse Treebank and Penn Discourse Treebank did it for discourse structure; dialogue-act corpora (SWBD-DAMSL, HCRC Map Task) and ISO 24617-2 did it for conversation. Formal citations belong to the related-work review; the names here are pointers.

## Mapping

| Treebank concept | DreamFace counterpart |
| --- | --- |
| Document | An agentic session, or a bounded task within it. |
| Raw text | The persisted session: messages, parts, and events ([Layer 0](context-ontology.md)). |
| Tokenization / sentence split | Layer 0 part and message boundaries, plus DreamFace sub-part segmentation for prose. |
| Parse / dependency tree | Segment containment hierarchy plus the work-item tree. |
| Function tags / semantic roles / discourse relations | Communicative-function, work-intent, and relationship labels. |
| Annotator guidelines | DreamFace annotation guide: per-label definitions, boundary criteria, examples. |
| Agreement (κ, α) | Same practice, plus unitizing agreement for span boundaries. |
| Versioned release | Corpus releases with stable segment IDs and a schema version. |
| Cross-lingual shared scheme (UD-style) | One functional scheme, per-language context treebanks. |

## Why treebank practice transfers

- **Guidelines first.** A label exists when its definition, boundary criteria, and examples are written down; annotators apply definitions, not intuitions.
- **Double annotation and adjudication.** Label reliability is measured (Cohen's κ for categorical labels, Krippendorff's α, including unitizing variants, for spans), disagreements are adjudicated, and guidelines are revised in response.
- **Stable identifiers and releases.** Annotations reference segments by ID; releases carry a schema version so downstream experiments are reproducible.
- **Shared scheme, many languages.** The UD model — one annotation scheme, per-language treebanks — is the practical path for the multilingual goal: it decouples "what counts as a goal or a tool result" from "how a goal is phrased in Estonian or Korean".

## Where DreamFace departs from a classic treebank

- **Multi-party, non-prose.** Sessions mix user, assistant, tool, and subagent voices, and much content is structured (tool input/output, diffs, snapshots), so syntactic trees do not apply; Layer 0 structure takes their place.
- **Stateful, append-only.** Sessions evolve and carry lifecycle state (`pending → completed`, compacted, superseded); classic treebanks annotate static text. DreamFace adds lifecycle and epistemic status labels.
- **Machine-generated text is in scope.** Assistant output and tool output are annotation targets, not just context.
- **Operational downstream task.** The annotation must ultimately feed a context-selection policy, which raises the stakes on annotation validity: a wrongly labeled segment can cause a harmful context omission.
- **Privacy and provenance.** Real sessions contain secrets and user data; corpus releases need licensing, consent, or synthesis — stricter than typical treebank licensing.

## Research implications

- The Markov hypothesis becomes precise: over a gold treebank, segment-label transition statistics are the analog of n-gram/PCFG statistics over parse trees, and can be evaluated the same way (held-out likelihood, downstream policy ablation).
- Annotation validity can be measured before any policy is trained: if annotators cannot agree on a label across languages, the label — not the annotators — needs redesign.
- The treebank framing gives the whitepaper a concrete methodology section and the multilingual goal a concrete distribution model.

**Status:** framing proposal. The annotation guide itself is future work, tracked through [RFC 0001](rfcs/0001-context-segments-and-work-item-graphs.md).
