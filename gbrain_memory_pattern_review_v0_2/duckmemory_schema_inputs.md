# DuckMemory Schema Inputs

Tables:
- tenants, sources, pages, page_revisions, chunks, links, tags, facts, takes, timeline_events, files, jobs, audits, citations, query_cache.

Critical fields:
- source_id on all memory tables,
- generation on pages,
- confidence/status fields on facts/takes,
- provenance on links/citations,
- actor/request metadata in audit rows.

Indexes:
- unique(source_id,slug), vector index on chunk embedding, lexical indexes on title/body, edge from/to, status/time indexes.

Constraints:
- foreign keys for source/page relations,
- enum checks for resolution/status fields,
- uniqueness constraints for dedup domains.

Migration strategy:
- snapshot baseline + incremental idempotent migrations + verify hooks.
