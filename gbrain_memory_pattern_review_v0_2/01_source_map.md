# 01 Source Map

## src/core
Purpose: operation semantics, storage adapters, cycles, facts, minions, schema-pack, audit.
Evidence:
- `src/core/operations.ts` — operation and error model.
- `src/core/engine.ts` — interface/types.
- `src/core/pglite-engine.ts`, `postgres-engine.ts` — engine behavior.
- `src/core/migrate.ts` — migration registry.
DuckMemory lesson: keep core as transport-agnostic domain layer.

## src/core/search
Purpose: retrieval stages and diagnostics.
Evidence:
- `hybrid.ts`, `keyword.ts`, `vector.ts`, `mode.ts`, `query-cache.ts`, `graph-signals.ts`, `explain-formatter.ts`.
DuckMemory lesson: stage decomposition + explain ledger is mandatory.

## src/mcp
Purpose: remote tool exposure.
Evidence:
- `server.ts`, `dispatch.ts`, `tool-defs.ts`, `http-transport.ts`, `rate-limit.ts`.
DuckMemory lesson: separate transport parsing from operation execution and trust context assignment.

## src/cli + src/commands
Purpose: local operator interface and command orchestration.
Evidence:
- `src/cli.ts`, `src/commands/search.ts`, `serve-http.ts`, `graph-query.ts`, `doctor.ts`.

## docs
Purpose: architecture, workflows, eval policy.
Evidence:
- `docs/architecture/brains-and-sources.md`, `docs/architecture/RETRIEVAL.md`, `docs/eval/SEARCH_MODE_METHODOLOGY.md`.

## skills
Purpose: routing and procedural workflows.
Evidence:
- `skills/RESOLVER.md`, `skills/conventions/brain-routing.md`, `skills/maintain/SKILL.md`.

## scripts
Purpose: build/check/test orchestration.
Evidence: `scripts/ci-local.sh`, `scripts/build-schema.sh`, `scripts/check-privacy.sh`, `scripts/run-e2e.sh`.

## tests
Purpose: behavior lock.
Evidence: `test/search/*`, `test/migrations-*.test.ts`, `test/facts-*.test.ts`, `test/supervisor.test.ts`.
