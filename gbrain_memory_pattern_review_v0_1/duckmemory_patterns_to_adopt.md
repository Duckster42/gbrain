# DuckMemory Patterns to Adopt

1. **Contract-first operations** from `src/core/operations.ts`.
2. **Two-axis routing** from `docs/architecture/brains-and-sources.md` + `skills/conventions/brain-routing.md`.
3. **Source-scoped schema design** (`source_id` pervasive across core data).
4. **Hybrid retrieval stage decomposition** (`src/core/search/*` modular pipeline).
5. **Explain formatter + attribution stamping** (`search/explain-formatter.ts`, tests).
6. **Graph provenance fields** in links schema.
7. **Generation-triggered cache invalidation** in pages + query-cache gate.
8. **Migration verify/idempotency concepts** in `migrate.ts`.
9. **Unified audit writer abstraction** (`audit/audit-writer.ts`).
10. **Explicit trust boundary semantics** across local CLI vs remote MCP contexts.
