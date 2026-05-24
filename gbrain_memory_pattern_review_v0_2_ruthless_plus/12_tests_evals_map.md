# 12 Tests Evals Map

Evidence categories:
- Retrieval: `test/search/*.test.ts`, `test/hybrid-search-lite.serial.test.ts`, `test/search.test.ts`.
- Graph: `test/traverse-graph-dedup.test.ts`, `test/search/graph-signals.test.ts`.
- Schema/migration: `test/migrations-*.test.ts`, `test/schema-bootstrap-coverage.test.ts`.
- Facts/takes: `test/facts-*.test.ts`, `test/takes-resolution.test.ts`.
- Security/privacy: `test/source-config-redact.test.ts`, `test/destructive-guard.test.ts`.
- Eval harnesses: `test/eval-*.test.ts`, `docs/eval/SEARCH_MODE_METHODOLOGY.md`, `docs/eval-bench.md`.

Gaps noted:
- no single consolidated test map doc linking every operation to tests.

DuckMemory required V0 tests:
- contract validation,
- routing precedence,
- source-scope enforcement,
- retrieval explain snapshots,
- cache invalidation,
- graph boost guardrails,
- consolidation idempotence,
- audit log emission on failures.
