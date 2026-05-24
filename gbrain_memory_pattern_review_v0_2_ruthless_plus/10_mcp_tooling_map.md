# 10 MCP Tooling Map

Evidence:
- `src/mcp/server.ts`, `dispatch.ts`, `tool-defs.ts`, `http-transport.ts`, `rate-limit.ts`
- shared ops: `src/core/operations.ts`
- tests: `test/whoami.test.ts`, `test/oauth-scope-probe.test.ts`, `test/facts-mcp-allowlist.serial.test.ts`

Map:
- tool-defs publish callable operations.
- dispatch normalizes and routes calls.
- http-transport enforces auth/transport-level handling.
- trust boundary depends on remote context threading.

DuckMemory bridge readiness:
- keep shared contract registry,
- keep explicit scope claims,
- default remote read-only unless write grants present.
