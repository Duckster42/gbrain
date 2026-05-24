# DuckMemory ↔ GBrain Parity Matrix (V0_1)

| GBrain Capability | GBrain Evidence | Why It Matters | DuckMemory Equivalent | Match / Exceed / Replace | Acceptance Test | Risk If Missed | Status |
|---|---|---|---|---|---|---|---|
| Operation contract model | `src/core/operations.ts` | single source of behavior | `duckmemory/core/contracts.ts` | Match | CLI and API invoke same contract IDs | behavior drift | Planned |
| Engine abstraction | `src/core/engine.ts` | backend swap without API drift | `storage/engine-interface.ts` | Match | same test suite passes on sqlite+pg | lock-in | Planned |
| Engine factory | `src/core/engine-factory.ts` | deployment flexibility | adapter loader | Replace | no conditional logic in handlers | runtime complexity | Planned |
| Brain routing axis | `docs/architecture/brains-and-sources.md` | tenant isolation | tenant routing layer | Match | query with tenant override resolves correctly | data bleed | Planned |
| Source routing axis | `skills/conventions/brain-routing.md` | corpus partitioning | source scoper | Match | source precedence tests | wrong corpus answers | Planned |
| Pages table model | `pglite-schema.ts` pages | canonical memory units | pages + revisions | Exceed | revision diff available | loss of provenance | Planned |
| Chunk model | `pglite-schema.ts` content_chunks | retrieval granularity | chunks table | Match | deterministic chunk reconstitution | poor recall | Planned |
| Vector retrieval | `search/vector.ts` | semantic recall | vector retrieval stage | Match | semantic benchmark pass | semantic misses | Planned |
| Lexical retrieval | `search/keyword.ts` | precise token matches | bm25/trgm stage | Match | exact term benchmark pass | poor precision | Planned |
| Fusion pipeline | `search/hybrid.ts` | quality from multiple signals | staged fusion | Match | score ordering fixture parity | unstable ranking | Planned |
| Exact-match boost | `intent-weights.ts` | obvious answers top-ranked | exact boost stage | Match | exact-title query top-1 | user distrust | Planned |
| Recency boost | `search/recency-decay.ts` | freshness | decay function | Match | recent item outranks stale tie | stale output | Planned |
| Salience boost | search stage + docs | priority memory | salience signal | Match | high-salience fixture uplift | noisy ranking | Planned |
| Graph adjacency boost | `search/graph-signals.ts` | structural relevance | graph stage | Match | linked cluster uplift test | missing context | Planned |
| Cross-source graph boost | `search/graph-signals.ts` | corroboration | source-diversity boost | Exceed | cross-source evidence query uplift | silo bias | Planned |
| Explain ledger | `search/explain-formatter.ts` | trust/debuggability | explain API | Match | stage-attribution snapshot test | black-box ranking | Planned |
| Query cache | `query-cache.ts` | latency/cost control | cache store | Match | hit-rate + correctness tests | high cost/latency | Planned |
| Cache invalidation by generation | `pglite-schema.ts` trigger + cache gate | stale prevention | generation checks | Match | updated page invalidates cache | stale answers | Planned |
| Links graph schema | `links` table + view | relationship substrate | edges table | Match | edge dedup + provenance tests | graph corruption | Planned |
| Tags model | `tags` table | lightweight facets | tags table | Match | tag query fixtures | lost discoverability | Planned |
| Timeline model | page timeline + batch input | temporal reasoning | events table | Exceed | bitemporal event tests | weak chronology | Planned |
| Facts extraction | `facts/*`, tests | structured knowledge | facts pipeline | Match | extraction fixture accuracy | unstructured sprawl | Planned |
| Takes model | `engine.ts` types + tests | attributed beliefs/quality | takes subsystem | Match | resolve quality states tests | no belief tracking | Planned |
| Citation repair workflow | `skills/citation-fixer/SKILL.md` | source integrity | citation checker | Exceed | broken citation repair test | hallucination risk | Planned |
| Consolidation phase | `cycle/phases/consolidate.ts` | entropy reduction | consolidation DAG | Match | idempotent consolidate replay | memory drift | Planned |
| Jobs/minions | `src/core/minions/*`, migrations | background orchestration | bounded jobs svc | Replace | queue lifecycle tests | async fragility | Planned |
| Audit writer | `audit/audit-writer.ts` | forensics | append-only audit | Exceed | audit chain verification | poor incident response | Planned |
| CLI/MCP operation parity | CLI + MCP files share ops | transport consistency | shared adapters | Match | same payload across transports | integration drift | Planned |
| Remote trust boundary | docs + context fields | prevent privilege leaks | explicit trust token | Exceed | missing trust => hard reject | security incident | Planned |
| Upload/path validators | `validateUploadPath` etc | filesystem safety | path policy module | Match | traversal/symlink test suite | RCE/data exfil | Planned |
| Source-scoped auth | `AuthInfo` source fields | tenant correctness | scoped auth claims | Match | unauthorized source denied | cross-tenant leakage | Planned |
| Script governance | `scripts/*` | ops reliability | typed task runner | Replace | task manifest validation | operational drift | Planned |
| Eval methodology | `docs/eval/*`, eval tests | quality stability | eval harness | Match | regression gate blocks degradation | silent quality drop | Planned |
| Observability | audit/search telemetry modules | debugging | telemetry API | Exceed | query trace and audit correlation | opaque failures | Planned |
