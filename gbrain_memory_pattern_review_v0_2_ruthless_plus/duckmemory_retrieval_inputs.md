# DuckMemory Retrieval Inputs

Required:
- lexical retrieval,
- structured filters (source/type/date/tags),
- optional vector retrieval,
- fusion/rerank stages,
- graph-aware boost,
- explain ledger,
- context-pack generator for downstream agents.

Evidence basis:
- GBrain `src/core/search/*` modules and search tests.

Acceptance:
- ranking quality regression suite,
- explain-field completeness checks,
- cache key and invalidation integrity tests.
