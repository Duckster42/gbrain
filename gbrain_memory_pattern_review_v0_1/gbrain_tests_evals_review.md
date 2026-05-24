# GBrain Tests and Evals Review

## Evidence of broad test coverage
Repository includes many test suites under `test/` spanning:
- search ranking and explainability (`test/search/*.test.ts`),
- migrations and schema (`test/migrations-*.test.ts`, `test/schema-bootstrap-coverage.test.ts`),
- facts/takes/enrichment (`test/facts-*.test.ts`, `test/takes-*.test.ts`),
- minions/supervisor (`test/supervisor.test.ts`, `test/subagent-handler.test.ts`),
- routing/resolver/source scope (`test/source-resolver-with-tier.test.ts`, `test/sources.test.ts`),
- security/privacy checks (`test/source-config-redact.test.ts`, privacy script tests).

## Eval/benchmark assets
- `docs/eval-bench.md`
- `docs/eval/SEARCH_MODE_METHODOLOGY.md`
- tests: `test/eval-replay.test.ts`, `test/eval-longmemeval.test.ts`, `test/eval-trajectory.test.ts`, `test/benchmark-search-quality.ts`.

## What this means for parity
DuckMemory cannot treat evals as optional. GBrain evidence shows retrieval and memory behavior are actively regression-tested with dedicated methodology docs and fixtures.

## DuckMemory required eval gates
- fixed query golden set with attribution checks,
- cross-version diff reports for ranking deltas,
- migration replay tests from frozen baselines,
- consolidation correctness fixtures,
- security scope tests for remote callers.
