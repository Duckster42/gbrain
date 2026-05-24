# 11 Security Runtime Map

## Classified findings

### Safe pattern
- path/slug/file validators in `operations.ts`.
- source-scoped auth fields in `AuthInfo`.
- privacy checks in scripts (`check-privacy.sh`, `check-source-config-leak.sh`).

### Needs rewrite
- broad shell/job orchestration surface (`src/core/minions/handlers/shell.ts`) for DuckMemory baseline.
- markdown policy-only routing without compile-time checks.

### Sandbox only
- any shell job, plugin loader, external ingestion adapters.

### Reject (for DuckMemory V0)
- implicit remote write capability without explicit write grants.

### Unknown/manual review
- all admin/dist artifacts under `admin/` and binary wasm usage implications.

Evidence:
- `src/core/operations.ts`
- `src/core/minions/*`
- `src/mcp/http-transport.ts`
- `scripts/check-privacy.sh`
