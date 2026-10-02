# RFC 0000: RFC process

- **Status:** Accepted
- **Authors:** DreamFace project
- **Created:** 2026-10-02
- **Target:** Research framing

## Summary

How DreamFace records changes to shared concepts, interfaces, schemas, and policies.

## Scope

An RFC is required for: new or changed segmentation labels, schema changes, retention-policy proposals, console-mode semantics, corpus release policy, and terminology that affects other artifacts. An RFC is not required for: additions within existing structures, typo fixes, or bounded questions and experiments (use issues).

## Lifecycle

`Draft → Proposed → Accepted | Rejected`, and an accepted RFC may later be `Superseded`.

- **Draft:** open for discussion; the file lives at `docs/rfcs/NNNN-slug.md`, created from [the template](rfc-template.md).
- **Proposed:** stable for review; referenced from an issue so discussion has a home.
- **Accepted:** for implementation-target RFCs, acceptance requires observable behavior and tests; for research-target RFCs, acceptance requires an evaluation plan or documented evidence.
- **Rejected / Superseded:** kept for the record; superseded RFCs link to their replacement.

## Numbering and files

- Numbers are `NNNN`, zero-padded, sequential, and never reused; `0000` is this process.
- One file per RFC; status changes are made by editing the RFC header plus a commit.
- Accepted RFCs are not silently edited — supersede with a new number instead.

## Decision record

Decisions and their rationale live in the RFC itself; issues track bounded questions; the whitepaper cites RFCs as design provenance.

## Compatibility

Changes to this process supersede this RFC.
