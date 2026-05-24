# 02 Operation Contract Map

Capability: unified operation contract.
Evidence:
- `src/core/operations.ts` — operation defs, `OperationError`, validators (`validateUploadPath`, `validatePageSlug`, `validateFilename`), `AuthInfo`.
- `src/core/engine.ts` — return/input structures consumed by operations.

CLI mapping:
Evidence:
- `src/cli.ts` — dispatch and formatter.
- `src/commands/*.ts` — command-to-operation bridges.

MCP mapping:
Evidence:
- `src/mcp/tool-defs.ts` — tool schema publication.
- `src/mcp/dispatch.ts` — operation invocation.
- `src/mcp/server.ts`/`http-transport.ts` — remote envelope and scope context.

Error model:
- typed codes in `operations.ts` (`invalid_params`, `permission_denied`, etc.).

Audit/log side effects:
Evidence:
- `src/core/audit/audit-writer.ts` and specialized audit modules.

DuckMemory match:
- contract-first op registry with typed errors/scopes and transport adapters.
DuckMemory exceed:
- machine-generated OpenAPI/tool schema from the same contract source.
