# RIVET_GBRAIN_MEMORY_PATTERN_REVIEW_V0_1 — Deep Static Review Summary

This pass repairs the shallow V0 bundle by anchoring capability claims to concrete repository evidence. The review remained static-only: inspected code, docs, tests, scripts; no installs, no test runs, no GBrain runtime execution.

## What GBrain Actually Is (Evidence-Based)

GBrain is a contract-first memory runtime where `src/core/operations.ts` is the central capability surface shared by CLI and MCP. Runtime calls route through engine abstractions in `src/core/engine.ts` and concrete backends in `src/core/pglite-engine.ts` and `src/core/postgres-engine.ts`. Schema state is represented in `src/core/pglite-schema.ts` plus migration registry in `src/core/migrate.ts`. Search behavior is composed from modules in `src/core/search/*` including `hybrid.ts`, `keyword.ts`, `vector.ts`, `mode.ts`, `query-cache.ts`, and `graph-signals.ts`. The trust boundary is explicit and repeated in docs (`AGENTS.md`, `CLAUDE.md`) and code paths (`OperationContext.remote` use in operations and MCP dispatch chain).

This means practical value is not just “vector DB + notes.” It is the integration of:
- operation contract + transport parity,
- multi-source routing model,
- hybrid retrieval pipeline with explain output,
- graph-aware post-fusion reranking,
- extraction/enrichment/consolidation loops,
- operational scripts and eval gates.

## Why V0 Was Insufficient

V0 reports gave coarse summaries but did not map claims to table/module/function-level evidence. For parity-or-better work, DuckMemory needs reproducible mappings: where concepts live, which modules mutate them, which tests pin behavior, and which scripts/docs encode operational assumptions.

## Main Findings

1. **Architecture discipline is real**: contract-first pattern is explicit in `operations.ts`, with shared behavior across CLI and MCP (`src/cli.ts`, `src/mcp/server.ts`, `src/mcp/dispatch.ts`, `src/mcp/tool-defs.ts`).
2. **Memory layout is multi-axis**: docs in `docs/architecture/brains-and-sources.md` and resolver conventions in `skills/conventions/brain-routing.md` define brain (DB) vs source (repo-in-DB). Data schema supports this with `source_id` across key tables.
3. **Schema is mature and heavily migrated**: `migrate.ts` shows long-tail compatibility handling and retry/verification machinery.
4. **Retrieval is layered and observable**: `search/hybrid.ts` orchestrates multi-stage ranking; `search/explain-formatter.ts` exports score attribution; `search/mode.ts` gates knobs and cache-key behavior.
5. **Graph is integrated into ranking**: links schema + traversal methods + `search/graph-signals.ts` stage.
6. **Consolidation/enrichment are first-class**: `src/core/cycle/*`, `src/core/facts/*`, `src/core/citation-fixer`-related skill/docs paths.
7. **Operational footprint is heavy**: script surface under `scripts/` is broad (build, checks, smoke, privacy, e2e orchestration).

## DuckMemory Parity-Or-Better Implication

DuckMemory should copy the behavior-level advantages while reducing baggage:
- Keep operation-contract discipline.
- Keep two-axis routing semantics.
- Keep hybrid + explain + graph stages.
- Keep auditable enrichment/consolidation DAG.
- Keep eval regression gates.
- Reduce installer/runtime complexity and markdown-only workflow drift.

## Non-Negotiable Replacement Rule

Any rejected GBrain behavior must map to:
1) better DuckMemory replacement, or
2) existing RIVET-native equivalent, or
3) explicit not-useful rationale.

That rule is enforced in the parity matrix and reject/replace documents in this folder.
