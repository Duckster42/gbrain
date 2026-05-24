# DuckMemory Test Eval Inputs

Required suites:
- unit: contracts/routing/validation/scoring stages.
- integration: storage engines, migrations, retrieval pipeline.
- retrieval: lexical/vector/fusion/graph/explain snapshots.
- graph: edge provenance/traversal/scope.
- schema: migration replay and constraint checks.
- security: auth scope, path traversal, remote trust fail-closed.
- parity: GBrain capability matrix row tests.
- regression: benchmark deltas and release gates.

Evidence baseline:
- `test/search/*`, `test/facts-*`, `test/migrations-*`, `test/source-*`, eval docs/harness files.
