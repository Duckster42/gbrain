# DuckMemory Clean-Room Spec Inputs (for RIVET_DUCKMEMORY_CLEANROOM_SPEC_V0)

## Recommended module tree
- `core/contracts/` (operation schemas, error model)
- `core/routing/` (tenant/source resolution)
- `core/storage/` (engine interface + implementations)
- `core/retrieval/` (keyword/vector/fusion/graph/explain/cache)
- `core/graph/` (edge store/traversal/provenance)
- `core/enrichment/` (extractors, validators, normalizers)
- `core/consolidation/` (dedupe, merge, citation repair, contradiction handling)
- `core/security/` (auth claims, trust context, path policy)
- `core/audit/` (append-only logs, correlation ids)
- `interfaces/cli`, `interfaces/api`, `interfaces/toolbridge`
- `eval/` (benchmarks, replay, regression gates)

## Recommended storage layout
- relational DB with strict source scoping and generation fields,
- optional vector extension,
- append-only audit/event tables,
- revision history for page bodies.

## Recommended tables/indexes
- tables: tenants, sources, pages, page_revisions, chunks, links, tags, facts, takes, timeline_events, files, jobs, audits, query_cache.
- indexes: unique(source_id,slug), hnsw/chunk vector idx, trgm/bm25 idx, JSONB GIN, page generation and updated_at indices, edge from/to indices, audit(kind,time).

## File memory layout
- `memory/` for local artifacts,
- `artifacts/eval/` for benchmark outputs,
- `audit/` for append-only logs,
- `workflows/` for versioned typed workflow specs.

## Operation contracts
- single registry with scope tags: read/write/admin/local-only,
- transport adapters consume same registry,
- mandatory trust context in every call envelope.

## Retrieval pipeline
- query normalize → lexical/vector retrieval → fusion → post-fusion boosts (exact, recency, salience, graph) → explain formatter → cache write.

## Graph model
- typed/provenanced edges with source scoping and traversal caps.

## Enrichment pipeline
- ingest text/chunks → entity extraction → fact/take extraction → validator pass → confidence scoring → write + audit.

## Consolidation DAG
- detect duplicates/aliases → merge/canonical redirect → citation repair → contradiction scan → timeline reconcile → emit consolidation receipt.

## Citation model
- citation table keyed by page+span+source URI/hash with repair status.

## Confidence/status model
- fact/take confidence float + status enums; resolution events retained historically.

## Audit model
- append-only JSONL/DB stream with signed digest chain and request correlation.

## CLI/API/tool surfaces
- CLI for local operators,
- HTTP API for controlled integrations,
- toolbridge (MCP-like) read-default / write-by-policy.

## RIVET/Patch Shop/SKYE hooks
- RIVET: deterministic retrieval and evaluation APIs.
- Patch Shop: UI endpoints for citation repairs, contradiction review, source-scoped graph views.
- SKYE: workflow trigger hooks for enrichment and consolidation receipts.

## Security model
- fail-closed trust context,
- least-privilege scopes,
- strict path validators,
- separate privileged worker for high-risk operations.

## Test/eval plan
- unit: contracts/routing/scoring,
- integration: storage + retrieval,
- e2e: CLI/API/tool parity,
- eval: golden query set, contradiction fixtures, migration replay baselines.

## V0 acceptance criteria
- operation registry + routing + pages/chunks/links/facts/takes,
- hybrid retrieval with explain,
- source-scoped auth,
- audit logs,
- baseline eval harness.

## V1 expansion criteria
- multimodal retrieval,
- advanced consolidation UX,
- richer schema packs and workflow marketplace,
- multi-tenant managed deployment hardening.
