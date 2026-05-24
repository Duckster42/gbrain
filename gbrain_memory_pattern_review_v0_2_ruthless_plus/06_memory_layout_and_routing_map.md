# 06 Memory Layout and Routing Map

Evidence:
- `docs/architecture/brains-and-sources.md`
- `skills/conventions/brain-routing.md`
- schema `source_id` fields in `pglite-schema.ts`
- source resolver tests: `test/source-resolver-with-tier.test.ts`

Brain/source model:
- Brain: DB boundary.
- Source: corpus boundary inside brain.

Routing precedence:
- documented flag/env/dotfile/path/default chain.

Memory objects:
- pages/chunks/links/tags/facts/takes/timeline/files/jobs/audit.
Evidence:
- schema and core modules: `pglite-schema.ts`, `engine.ts`, `facts/*`, `minions/*`, `audit/*`.

DuckMemory match:
- two-axis routing, source-scoped identity, audit-aware writes.
DuckMemory exceed:
- enforce routing on all writes via capability policy engine.
