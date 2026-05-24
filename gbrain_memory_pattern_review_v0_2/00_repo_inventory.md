# 00 Repo Inventory

## Top-level tree (observed)
`admin/`, `docs/`, `skills/`, `scripts/`, `src/`, `test/`, `tests/`, `evals/`, `examples/`, `templates/`, prior review folders.

## Counts
- Total tracked files (rg): 1928.
- `src/`: 584.
- `test/`: 890.
- `docs/`: 96.
- `scripts/`: 56.
- `skills/`: 118.

## Extension profile (sampled)
- Source: `.ts`, `.sql`, `.md`, `.json`, `.sh`, `.mjs`.
- Binary/native-looking: `src/assets/wasm/*.wasm`, grammar wasm payloads.

## Package/config files
- `package.json`, `bun.lock`, `gbrain.yml`, `docker-compose.test.yml`, `.env.testing.example`.

## Security-sensitive-looking files
- `src/core/operations.ts` (path/file validators)
- `src/mcp/http-transport.ts` (remote ingress)
- `src/core/minions/handlers/shell.ts` and `shell-redact.ts`
- `scripts/check-privacy.sh`, `scripts/check-source-config-leak.sh`

## Files reviewed in depth
- `src/core/operations.ts`, `engine.ts`, `pglite-schema.ts`, `migrate.ts`
- `src/core/search/hybrid.ts`, `graph-signals.ts`, `query-cache.ts`, `explain-formatter.ts`, `mode.ts`
- `src/mcp/server.ts`, `dispatch.ts`, `tool-defs.ts`, `http-transport.ts`
- `skills/RESOLVER.md`, `skills/conventions/brain-routing.md`
- `docs/architecture/brains-and-sources.md`, `docs/eval/SEARCH_MODE_METHODOLOGY.md`
- script inventory under `scripts/`
- test inventories in `test/` including search/migration/facts/minions/security suites

## Files skimmed
- broader docs in `docs/guides/*`, `docs/designs/*`
- command files under `src/commands/*`

## Not reviewed line-by-line
- all 890 test files, all wasm assets, `admin/node_modules/` and build artifacts.

## Why not
Volume and irrelevance to static behavior mapping granularity; sampled where needed for evidence.
