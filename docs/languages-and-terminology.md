# Languages and terminology

DreamFace intends to study context segmentation across languages, not just translate an English taxonomy. Segmentation boundaries, morphology, discourse conventions, and tool text can vary substantially across languages.

## Corpus plan

1. Begin with a language-neutral annotation schema and an English pilot corpus.
2. Add languages based on research access and reviewer competence; record language and script at segment level where text is mixed.
3. Use parallel examples where available, but also collect naturally occurring examples so the corpus does not equate translation with native usage.
4. Document each collection's source, consent/authorization, license, transformations, exclusions, and known biases.
5. Use independent annotators and record disagreement for labels whose interpretation is not obvious.
6. Structure releases as an [agentic context treebank](context-treebank.md): stable segment IDs, schema versions, agreement reporting, and per-language releases under the shared scheme.

Do not place private conversations, credentials, or identifying tool output into a public corpus. Prefer synthetic or explicitly licensed examples for repository-hosted fixtures.

## Terminology register

Maintain a shared register with a stable concept identifier, preferred term, definition, scope note, examples, source, and language-specific preferred/alternate terms. The register is seeded as machine-readable data in [terminology/concepts.yml](../terminology/concepts.yml) with stable concept identifiers (`DF-T-NNN`). The English terms in the project are provisional until reviewed.

Initial concepts to register:

| Concept | Provisional definition |
| --- | --- |
| Context segment | A bounded span or structured unit of conversation context with provenance. |
| Work item | A bounded unit of work with an outcome and a verification condition. |
| Delegative intent | Assignment of an outcome or responsibility to an actor. |
| Procedural intent | Specification of a method or workflow. |
| Imperative intent | A concrete action request or command. |
| Context retention | A policy decision to keep, compress, retrieve, or omit a segment for a particular operation. |

## EU terminology and role vocabulary

Use clear, inclusive role names and keep role labels distinct from legal or employment classifications. When useful, map research vocabulary to maintained EU multilingual resources (for example, IATE terminology or ESCO occupation/skill concepts), recording the resource version and mapping rationale. Such mappings are references for interoperability, not a claim of legal or regulatory compliance.

## Interoperability

Prefer stable concept IDs and language tags (BCP 47) alongside human-readable labels. Keep the source language and original span when adding translations. Publish annotation guidance and version changes with the corpus so other labs can reproduce or adapt it.
