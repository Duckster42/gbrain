# GBrain Consolidation Review

## Evidence modules and docs
- `src/core/cycle/phases/consolidate.ts`
- `src/core/cycle.ts`
- `src/core/facts/*` (canonicalization/migration support patterns)
- `src/core/link-extraction.ts`
- docs: `docs/contradictions.md`, `docs/guides/compiled-truth.md`, `docs/eval-takes-quality.md`
- tests: `test/cycle-synthesize.test.ts`, `test/cycle-synthesize-chunker.test.ts`, `test/eval-contradictions-integrations.test.ts`, `test/takes-resolution.test.ts`

## Consolidation tasks observed
- merge extracted structure back into canonical page representations,
- keep facts/takes aligned with current canonical entities,
- update timelines and references,
- maintain contradiction surfacing and quality scoring paths.

## Citation and contradiction handling
Skills and docs include citation repair and contradiction probes (`skills/citation-fixer/SKILL.md`, `docs/proposals/temporal-contradiction-probe.md`). Consolidation therefore sits in a larger review/remediation loop, not isolated ETL.

## Manual review pathways
- skills like `skills/maintain/SKILL.md`, `skills/frontmatter-guard/SKILL.md`, `skills/citation-fixer/SKILL.md`
- doctor and eval commands documented in `docs/GBRAIN_VERIFY.md`, `docs/eval-bench.md`

## DuckMemory parity targets
1. Idempotent consolidate pass with checkpoint IDs.
2. Alias/canonical redirect table for entity merges.
3. Citation integrity checker with repair receipts.
4. Contradiction detector that emits explainable conflict records.
5. Replayable consolidation logs (inputs, transforms, outputs).
