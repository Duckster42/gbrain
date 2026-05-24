# GBrain Retrieval and Search Review

## Pipeline modules (code evidence)
- Orchestration: `src/core/search/hybrid.ts`
- Lexical: `src/core/search/keyword.ts`
- Vector: `src/core/search/vector.ts`
- Query expansion: `src/core/search/expansion.ts`
- Intent weighting/exact match: `src/core/search/intent-weights.ts`, `query-intent.ts`, `llm-intent.ts`
- Dedup: `src/core/search/dedup.ts`
- Graph stage: `src/core/search/graph-signals.ts`
- Mode/knobs: `src/core/search/mode.ts`, `mode-switch-ux.ts`
- Cache: `src/core/search/query-cache.ts`, `query-cache-gate.ts`
- Explain output: `src/core/search/explain-formatter.ts`
- Telemetry/eval: `src/core/search/telemetry.ts`, `eval.ts`

## End-to-end behavior map
1. User/tool submits query via CLI/MCP operation.
2. Query options include source scope, limit/offset, mode knobs.
3. Expansion/intent modules may adjust weighting.
4. Keyword and vector candidate sets are retrieved.
5. Fusion and dedup compose combined candidate list.
6. Post-fusion stages apply boosts/demotions (backlink, salience, recency, exact match, graph signals).
7. Optional reranking and attribution fields are stamped on results.
8. Explain formatter emits per-result contribution lines.
9. Cache store/read path gated by knob hash + page generations to avoid stale cross-mode contamination.

## Explainability evidence
`explain-formatter.ts` is dedicated formatter; attribution stamping tests exist (`test/search/attribution-stamping.test.ts`, `test/search/explain-formatter.test.ts`, `test/search/graph-signals-wire-integration.test.ts`). This means explain is not accidental; it is a supported output contract.

## Mode behavior evidence
`mode.ts` includes knob bundles and versioned hash keying for cache partitioning. Tests like `test/search/knobs-hash-reranker.test.ts` indicate behavior lock.

## Retrieval quality guardrails
- Search tests: `test/search.test.ts`, `test/hybrid-search-lite.serial.test.ts`, `test/search-telemetry.test.ts`.
- Benchmark harness artifact: `test/benchmark-search-quality.ts`.
- Methodology docs: `docs/eval/SEARCH_MODE_METHODOLOGY.md`.

## DuckMemory parity requirements
- Preserve dual-channel retrieval (lexical+vector).
- Preserve deterministic post-fusion stage order.
- Preserve attribution fields for every stage.
- Preserve cache separation by mode knobs and corpus generation.
- Preserve explicit query-mode controls for cost/quality tradeoffs.

## DuckMemory exceed opportunities
- deterministic numeric replay mode with frozen embeddings,
- pluggable scorer registry with signed config snapshots,
- built-in calibration report per deployment.
