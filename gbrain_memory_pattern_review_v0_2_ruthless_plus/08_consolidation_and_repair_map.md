# 08 Consolidation and Repair Map

Evidence:
- `src/core/cycle/phases/consolidate.ts`
- `src/core/cycle.ts`
- `src/core/facts/*` for canonicalization/fence sync
- skills: `skills/citation-fixer/SKILL.md`, `skills/maintain/SKILL.md`
- docs: `docs/contradictions.md`, `docs/eval-takes-quality.md`

Covered behaviors:
- dedup and merge paths,
- citation repair workflow,
- alias/canonical handling (facts migration helpers noted in engine comments/types),
- stale/superseded handling through takes/facts status,
- contradiction checks and eval surfaces,
- manual review via skills + doctor/eval commands.

DuckMemory requirements:
- replayable consolidation DAG receipts,
- canonical redirect table,
- contradiction records with evidence pointers,
- citation repair audit entries.
