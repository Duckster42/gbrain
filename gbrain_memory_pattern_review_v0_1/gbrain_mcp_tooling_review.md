# GBrain MCP and Tooling Review

## Core MCP files
- `src/mcp/server.ts`
- `src/mcp/dispatch.ts`
- `src/mcp/http-transport.ts`
- `src/mcp/tool-defs.ts`
- `src/mcp/rate-limit.ts`

## Shared operation surface
Both CLI and MCP call into operation handlers defined in `src/core/operations.ts`. This prevents drift between local and remote capability semantics.

## Transport/trust boundaries
- Local CLI context sets trusted caller path (`remote=false`) per architecture docs and comments.
- MCP/HTTP paths set remote context (`remote=true`) with auth and scope checks.
- Security-sensitive operations include local-only or stricter validation behavior.

## Auth/scope evidence
- `operations.ts` `AuthInfo` includes scopes and source restrictions.
- tests: `test/oauth-scope-probe.test.ts`, `test/operation-context-sourceid-required.test.ts`, `test/facts-mcp-allowlist.serial.test.ts`.

## Rate-limiting and observability
- Rate-limit module exists.
- request logs/audit logs exist via tables and audit modules.

## DuckMemory MCP stance
- Keep shared operation contracts.
- Keep strict remote defaults (fail-closed on missing trust context).
- Separate internal admin-only operations from remote tool set.
- Add explicit capability manifests per client.
