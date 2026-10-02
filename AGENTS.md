# AGENTS.md — DreamFace agent conventions

Conventions for AI agents (opencode or others) working in this repository.

## Project shape

- Research-first repository: docs, RFCs, schemas, terminology, and future prototypes.
- Everything proposed is a hypothesis unless explicitly marked implemented and evaluated. Never present a design as a demonstrated result.

## Evidence rules

- Layer 0 claims about the OpenCode schema must cite a pinned release or commit of `anomalyco/opencode` with an access date; do not base implementation decisions on mutable branch heads.
- Corpus material must be synthetic or explicitly licensed; never add real session data containing secrets or personal data (see `docs/languages-and-terminology.md`).

## Change process

- Shared concepts, schemas, and interfaces change through an RFC (`docs/rfcs/0000-rfc-process.md`); additions within existing structures do not.
- Terminology: new concepts get the next free stable ID in `terminology/concepts.yml`; never renumber.
- Schemas: version per `schema/README.md`.

## Commits

- Short, concise subject lines.
- No `Co-Authored-By:` trailers or other agent-attribution lines in commit messages.

## Verification

- Docs: after renames, check that relative links still resolve.
- Schemas: validate against the examples in `schema/examples/` before committing.
- Site: GitHub Pages builds from `docs/` (Jekyll/minima); check the Pages build after structural changes.

## Working mode

Default mode for agents on this repo: **Build** — bounded increments with user verification at checkpoints.
