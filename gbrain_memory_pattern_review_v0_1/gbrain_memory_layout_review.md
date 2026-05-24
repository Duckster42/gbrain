# GBrain Memory Layout Review

## Concept map and evidence

### Brains (database-level boundary)
- Evidence: `docs/architecture/brains-and-sources.md`, `skills/conventions/brain-routing.md`, `src/core/brain-registry.ts`.
- Purpose: isolate full memory stores by owner/team/access policy.

### Sources (repo-in-brain boundary)
- Evidence: `sources` table in `src/core/pglite-schema.ts`, source resolver tests (`test/source-resolver-with-tier.test.ts`, `test/sources.test.ts`).
- Purpose: partition corpora within a brain and scope read/write.

### Pages
- Evidence: `pages` table schema in `pglite-schema.ts`; engine methods in `engine.ts`.
- Content: slug/type/title/frontmatter/compiled_truth/timeline/content hash/salience fields/generation.

### Content chunks
- Evidence: `content_chunks` table, embedding columns (`embedding`, `embedding_image`, `embedding_multimodal`), indexes in schema; search modules reference chunk retrieval.
- Purpose: retrieval granularity and embedding substrate.

### Links
- Evidence: `links` table fields: `link_type`, `context`, `link_source`, `origin_page_id`, `origin_field`, `resolution_type`; `page_links` view.
- Purpose: graph connectivity + provenance.

### Tags
- Evidence: `tags` table and indexes.

### Facts and Takes
- Evidence: types in `engine.ts` (`Take`, `TakeBatchInput`, resolution fields); facts modules in `src/core/facts/*`; tests (`test/facts-engine.test.ts`, `test/takes-resolution.test.ts`).

### Timeline
- Evidence: timeline columns in `pages`; batch timeline input types in `engine.ts`; extraction module `link-extraction.ts` and tests around frontmatter/extraction.

### Files
- Evidence: `files` support referenced in `engine.ts` and migration comments; `file_migration` tests.

### Jobs
- Evidence: `minion_jobs` and `minion_inbox` migrations in `migrate.ts`; runtime in `src/core/minions/*`.

### Audit records
- Evidence: `src/core/audit/audit-writer.ts`, rerank/shell/supervisor/slug-fallback audits.

## Routing/scoping model
- Brain resolution and source resolution are layered precedence systems documented in `skills/conventions/brain-routing.md`.
- Remote callers are scoped by auth context rather than local dotfiles, documented in same file and reflected in operation context comments.

## DuckMemory parity target
- Keep orthogonal routing axes.
- Store source_id on all memory-bearing tables.
- Retain provenance fields on edges/facts.
- Keep generation/version columns to support cache invalidation and replay.
