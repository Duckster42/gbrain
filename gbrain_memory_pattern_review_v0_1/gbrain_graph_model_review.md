# GBrain Graph Model Review

## Storage and schema evidence
- Edge table: `links` in `src/core/pglite-schema.ts`.
- Key fields: `from_page_id`, `to_page_id`, `link_type`, `context`, `link_source`, `origin_page_id`, `origin_field`, `resolution_type`.
- Alias view: `page_links` for compatibility query paths.

## Provenance and repair semantics
`link_source` and `origin_page_id` provide extraction provenance (markdown/frontmatter/manual). This supports selective cleanup/rebuild without deleting unrelated edges. `origin_field` supports frontmatter-driven relation mapping.

## Traversal evidence
`src/core/engine.ts` exposes `traverseGraph` and `traversePaths` with `sourceId`/`sourceIds` options and `frontierCap` for bounded expansion. Tests like `test/traverse-graph-dedup.test.ts` indicate dedup semantics are pinned.

## Ranking coupling
`src/core/search/graph-signals.ts` applies graph-adjacency and cross-source boosts to retrieval candidates. `src/core/search/hybrid.ts` integrates this stage in post-fusion pipeline.

## Constraints and risks
- Graph quality depends on extraction freshness (`link-extraction.ts` paths + maintenance cycles).
- Over-boost risks are mitigated by score-floor gates in graph stage tests.
- Cross-source boosts may be dormant in single-source brains; design should degrade gracefully.

## DuckMemory graph requirements
1. Edge provenance mandatory.
2. Source-scoped traversal filters mandatory.
3. Bounded traversal controls mandatory.
4. Ranking-integration should be explainable per result.
5. Graph rebuild and edge repair should produce audit trails.
