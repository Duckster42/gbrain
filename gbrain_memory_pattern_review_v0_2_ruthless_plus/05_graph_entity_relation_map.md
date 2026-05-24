# 05 Graph Entity Relation Map

Evidence:
- `links` schema in `src/core/pglite-schema.ts`
- traversal opts in `src/core/engine.ts` (`TraverseGraphOpts`, source scope, frontier cap)
- ranking coupling in `src/core/search/graph-signals.ts`
- extraction source in `src/core/link-extraction.ts`

Entity carriers:
- pages are primary node type (person/company/project/system represented via page type/frontmatter conventions).

Relation model:
- directed edges `from_page_id -> to_page_id` with `link_type`, `context`, `link_source`, `origin_page_id`, `origin_field`, `resolution_type`.

Graph-in-ranking:
- adjacency and cross-source boosts/demotions applied post-fusion.

Supersession/stale evidence:
- takes/facts status fields in `engine.ts` types; consolidation modules in `src/core/cycle/phases/consolidate.ts`.

DuckMemory graph inputs:
- graph tables: nodes (pages) + edges + edge_evidence.
- confidence/provenance required per edge.
- supersession relation for stale claims.
- acceptance tests: edge dedup, provenance retention after rebuild, graph boost guardrails.
