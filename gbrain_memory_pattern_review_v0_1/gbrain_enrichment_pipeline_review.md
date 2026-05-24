# GBrain Enrichment Pipeline Review

## Evidence modules
- `src/core/cycle/extract-facts.ts`
- `src/core/facts/extract.ts`
- `src/core/facts/extract-from-fence.ts`
- `src/core/cycle/extract-takes.ts`
- `src/core/think/entity-extract.ts`
- docs: `docs/guides/enrichment-pipeline.md`, `docs/takes-vs-facts.md`, `docs/guides/entity-detection.md`
- tests: `test/facts-extract.test.ts`, `test/facts-engine.test.ts`, `test/facts-classify.test.ts`, `test/facts-backstop-gating.test.ts`

## What is extracted
- entity references,
- typed fact rows (metrics/events depending on schema/fence model),
- takes (attributed assertions with holder/weight/time and resolution state),
- links/timeline via extraction path in `link-extraction.ts`.

## Confidence/signal handling
`engine.ts` take types show weight and resolution states (`correct/incorrect/partial/unresolvable`) and supporting fields (`resolved_source`, `resolved_by`). This indicates evidence-tracked adjudication rather than binary pass/fail.

## Failure/audit handling
- `audit-writer.ts` unifies JSONL audit streams.
- `facts/phantom-audit.ts`, `facts/stub-guard-audit.ts`, `audit-slug-fallback.ts` capture notable fallbacks/errors.

## External/runtime assumptions
Enrichment can involve embeddings and provider integrations (see docs under `docs/integrations/*`, `docs/ai-providers/*`), but static architecture supports local flows with provider-optional pipelines.

## DuckMemory local-first design
- Build extraction DAG that can run fully local with optional remote enrichers.
- Persist raw extraction trace + normalized facts/takes + adjudication events.
- Require audit record for every extraction fallback or parser failure.
- Provide deterministic “replay extraction” on a frozen corpus.
