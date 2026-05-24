# GBrain Database + Index Review
- Uses pgvector + HNSW for vector columns; GIN/trigram for lexical routes.
- Schema includes source-scoped uniqueness (`source_id`,`slug`) and generation-based cache invalidation.
- Rich migration history indicates real production hardening and edge-case recovery.
- Indexing strategy includes partial indexes for modality-specific retrieval and lifecycle sweeps.
- DuckMemory guidance: keep multi-index hybrid retrieval (vector + lexical + metadata filters), but simplify migration graph and eliminate non-essential global-install assumptions.
