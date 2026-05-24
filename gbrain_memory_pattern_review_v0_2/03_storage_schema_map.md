# 03 Storage Schema Map

Primary schema evidence:
- `src/core/pglite-schema.ts`
- `src/schema.sql`
- `src/core/migrate.ts`
- execution details: `src/core/pglite-engine.ts`, `src/core/postgres-engine.ts`

## Core objects
- `sources`: id/name/local_path/config/archive fields.
- `pages`: source-scoped slug identity, content fields, salience/recency fields, generation.
- `content_chunks`: embeddings (`embedding`, `embedding_image`, `embedding_multimodal`), modality, symbol metadata.
- `links`: edge/provenance fields.
- `tags`, `raw_data`, auth tables, audit-related tables, query cache related tables, files table (via schema/migrations), jobs via migrations.

## Index/constraint evidence
- unique `(source_id, slug)` on pages.
- HNSW indexes on embedding columns.
- GIN/trgm/jsonb indexes in pages/frontmatter/title paths.
- link uniqueness and from/to indexes.
- generation bump trigger for cache invalidation.

## Migration behavior
- `migrate.ts` defines ordered versions, idempotence semantics, verify hooks, retry exhaust envelopes.

DuckMemory schema mapping:
- Match: source-scoped page identity, chunk vectors, edge provenance, generation invalidation.
- Exceed: first-class revision/event tables, explicit citation row model.
Acceptance tests:
- migration replay from baseline snapshot.
- cache invalidation trigger correctness on content updates.
- source isolation across slug collisions.
