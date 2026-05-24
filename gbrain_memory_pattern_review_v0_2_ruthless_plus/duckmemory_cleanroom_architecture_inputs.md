# DuckMemory Cleanroom Architecture Inputs

Module tree:
- core/contracts, core/routing, core/storage, core/retrieval, core/graph, core/enrichment, core/consolidation, core/security, core/audit, interfaces/cli, interfaces/api, interfaces/tools.

Control flow:
- ingress (cli/api/tool) -> contract validation -> auth/scope routing -> operation handler -> storage/query/retrieval -> audit emit -> response formatter.

Operation contracts:
- include scope tags (read/write/admin/local-only), explicit error codes, and deterministic JSON schema.

Engine boundary:
- storage interface mirroring page/chunk/link/fact/take/job/audit operations.

Storage boundary:
- source-scoped relational core; optional vector extension.

Surfaces:
- CLI for operators; API/tool for integrations with read-default policy.

RIVET integration points:
- retrieval explain API, parity-eval report API, consolidation receipt API.
