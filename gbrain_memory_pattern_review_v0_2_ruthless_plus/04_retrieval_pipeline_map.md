# 04 Retrieval Pipeline Map

Evidence:
- `src/core/search/hybrid.ts` — orchestration and post-fusion stages.
- `keyword.ts` — lexical retrieval.
- `vector.ts` — embedding retrieval.
- `mode.ts` — mode knobs and hash versioning.
- `query-cache.ts`, `query-cache-gate.ts` — cache behavior.
- `graph-signals.ts` — graph-based boosts/demotions.
- `intent-weights.ts`, `query-intent.ts`, `llm-intent.ts` — intent/exact-match tuning.
- `explain-formatter.ts` — explain output surface.

Flow:
1. input query + scope + mode.
2. expansion/intent weighting.
3. lexical + vector candidate fetch.
4. fusion and dedup.
5. post-fusion boosts: exact/salience/recency/graph.
6. optional rerank deltas.
7. explain formatting.
8. cache read/write gated by knob hash and page generations.

Coverage evidence:
- `test/search/explain-formatter.test.ts`
- `test/search/graph-signals.test.ts`
- `test/search/knobs-hash-reranker.test.ts`
- `test/hybrid-search-lite.serial.test.ts`

DuckMemory requirements:
- full explain ledger,
- deterministic stage order,
- separate mode keys,
- generation-aware cache invalidation.
