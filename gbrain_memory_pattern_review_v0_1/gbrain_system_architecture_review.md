# GBrain System Architecture Review (Static)

## Primary control-plane modules
- `src/core/operations.ts`: canonical operation definitions, schemas, handler wiring, error envelope (`OperationError`), path/slug validators, trust-aware behavior gates.
- `src/core/engine.ts`: `BrainEngine` interface and shared types (pages, links, chunks, takes, traversal opts).
- `src/core/engine-factory.ts`: backend selection for pglite/postgres.
- `src/cli.ts` + `src/commands/*`: CLI entry and command adapters.
- `src/mcp/server.ts`, `src/mcp/dispatch.ts`, `src/mcp/http-transport.ts`, `src/mcp/tool-defs.ts`, `src/mcp/rate-limit.ts`: MCP and HTTP tool exposure.

### Role / Inputs / Outputs / Side effects
- **operations.ts** role: contract boundary. Input: normalized params + `OperationContext`. Output: typed operation payloads and errors. Side effects: page writes, chunk upserts, link extraction, search reads, file metadata operations, queue/job submission.
- **engine modules** role: DB abstraction. Input: operation-level data. Output: persisted rows / search result rows / graph traversals. Side effects: SQL execution and migration triggers.
- **CLI/MCP transport** role: user/tool ingress. Inputs: argv or tool call JSON. Output: formatted result JSON/human text. Side effects: audit logging, auth/scope enforcement, remote/local trust derivation.

## Data-plane and schema control
- `src/core/pglite-schema.ts`: full schema template for embedded engine; includes tables for sources/pages/chunks/links/tags/raw_data/files/oauth/minions/query cache and indexes/triggers.
- `src/core/schema-embedded.ts`: schema source for embedded distribution parity.
- `src/core/migrate.ts`: ordered migration registry with idempotence, verify hooks, retry envelopes (`MigrationRetryExhausted`), and drift handling (`MigrationDriftError`).

## Search/retrieval architecture
- Query path modules under `src/core/search/`: `keyword.ts`, `vector.ts`, `hybrid.ts`, `intent-weights.ts`, `mode.ts`, `query-cache.ts`, `graph-signals.ts`, `explain-formatter.ts`, `telemetry.ts`, `eval.ts`.
- This indicates a staged architecture rather than monolithic scoring SQL.

## Enrichment/consolidation architecture
- `src/core/cycle/*`: phase-oriented maintenance flow (`extract-facts.ts`, `extract-takes.ts`, `phases/consolidate.ts`, `schema-suggest.ts`).
- `src/core/facts/*`: fact extraction and fence conversion logic.
- `src/core/link-extraction.ts`: markdown/frontmatter link/timeline extraction.

## Background jobs/minions
- `src/core/minions/*`: queue, supervisor, worker, handler registry, rate leases, budgets, quiet-hours, shell/subagent handlers, audits.
- Migration evidence in `migrate.ts` (`minion_jobs`, `minion_inbox`) confirms persistent job orchestration plane.

## Skill/workflow architecture
- `skills/RESOLVER.md`: dispatcher table.
- `skills/*/SKILL.md`: protocol assets.
- `skills/conventions/*`: cross-cutting policy (brain-first, routing, quality, search modes).

## Docs as architecture constraints
- `CLAUDE.md`, `AGENTS.md`: trust boundary and operating model.
- `docs/architecture/brains-and-sources.md`, `docs/architecture/RETRIEVAL.md`, `docs/designs/MINIONS_AGENT_ORCHESTRATION.md`, `docs/guides/*` define expected workflows.

## DuckMemory lessons
1. Preserve contract-first op schema as single source.
2. Separate transport from policy enforcement.
3. Keep storage engine behind narrow interface.
4. Make retrieval stage decomposition explicit with per-stage attribution.
5. Keep maintenance DAG separate from user query path.

## Baggage / risk to avoid
- Broad script/workflow sprawl increases drift risk.
- Markdown-only workflow routing can diverge from runtime behavior.
- Mixed trust context across transports requires strict fail-closed defaults.
- Large migration lineage can become operationally fragile without compaction strategy.
