# GBrain System Architecture Review
- Core pattern: `operations.ts` defines shared contract for CLI + MCP.
- Engines: pluggable `pglite` and `postgres` via engine factory.
- Explicit trust boundary: `OperationContext.remote` influences sensitive ops.
- Heavy emphasis on migration-forward compatibility and fail-open telemetry for non-critical stages.
- Architecture strength: behavior portability across transports.
- Architecture risk: broad runtime matrix (local cli, mcp stdio, mcp http, minion jobs) raises surface area.
