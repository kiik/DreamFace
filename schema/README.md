# Schemas

Draft 0.1 machine-readable artifacts for the DreamFace records described in [docs/context-ontology.md](../docs/context-ontology.md) and [docs/console-modes.md](../docs/console-modes.md).

- `segment.schema.json` — a derived annotation over Layer 0 (JSON Schema 2020-12)
- `work-item.schema.json` — a node of the work-item graph
- `examples/` — one minimal valid instance per schema, usable as fixtures

## Versioning

- Schemas are `0.x` drafts and may change; corpus releases must record the schema commit they used.
- Renames, removals, or semantic changes to existing fields go through an RFC ([RFC process](../docs/rfcs/0000-rfc-process.md)).
- Additive changes bump the draft minor version and are noted in the release.

## Validation

Any JSON Schema 2020-12 validator works; for example with Python `jsonschema`:

```sh
python3 -c 'import json, jsonschema; jsonschema.validate(instance=json.load(open("examples/segment.json")), schema=json.load(open("segment.schema.json")))'
```
