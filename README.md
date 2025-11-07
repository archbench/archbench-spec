# ArchBench Specification

Source of truth for the DSL contracts shared across the engine, frontend, and content packs.

## Schema versions

| File | Notes |
| --- | --- |
| `schema/archbench.v0.json` | Legacy draft with only names/nodes/edges. |
| `schema/archbench.v1.json` | Adds workload targets, node performance knobs, and database config support. |

## Examples

Sample scenarios that must always validate against the latest schema live in `examples/`.

| Scenario | File |
| --- | --- |
| URL Shortener | `examples/url-shortener.json` |
| Chat DM | `examples/chat-dm.json` |
| Checkout | `examples/checkout.json` |

## Validation CLI

We use `ajv-cli` to run validations locally and in CI.

```bash
npm install
npm run validate
```

The command expands `examples/*.json`, so any new scenario JSONs dropped into that folder automatically become part of the contract test suite. To validate an arbitrary file, run:

```bash
npm exec ajv validate --spec=draft2020 -s schema/archbench.v1.json -d path/to/file.json --strict=false
```

## Contributing

1. Update or add schemas under `schema/`.
2. Provide at least one example referencing new fields.
3. Run `npm run validate` before opening a PR.
