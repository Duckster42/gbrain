# GBrain Database and Index Review

## Schema evidence baseline
Primary schema evidence is in `src/core/pglite-schema.ts` and migration evolution in `src/core/migrate.ts`.

Key tables visible in schema text and migration registry include:
- `sources`
- `pages`
- `content_chunks`
- `links` (+ `page_links` view)
- `tags`
- `raw_data`
- auth tables (`oauth_clients`, tokens/codes, access tokens)
- request log tables
- minion/job tables from migration chain

## Indexing patterns
- B-tree: source/type/date/status fields.
- GIN trgm: `pages.title` search acceleration.
- GIN JSONB: `pages.frontmatter` querying.
- HNSW vector indexes: chunk embedding columns, including modality-specific partial indexes.
- Partial indexes: deleted rows purge scans, non-null modality indexes.
- Unique constraints: `(source_id,slug)` for page identity; dedupe constraints for links and chunk indexes.

## Cache invalidation mechanics
- `pages.generation` and trigger `bump_page_generation_fn` in schema provide content-change versioning.
- Query cache modules (`src/core/search/query-cache.ts`, `query-cache-gate.ts`) leverage generation checks and mode-key segregation (`mode.ts` knob hash versioning).

## Migration mechanics
`src/core/migrate.ts` includes:
- ordered migration list with version/name/sql/handler,
- optional engine-specific SQL,
- transaction toggles,
- idempotence classification,
- verify hooks,
- retry exhaustion with blocker diagnostics.

This is important for long-lived local brains and hosted DBs with partial upgrade history.

## DuckMemory table proposal (parity-oriented)

| Table | Purpose | Critical fields | Indexes | GBrain parity source | Exceed target |
|---|---|---|---|---|---|
| tenants | Brain-level boundary | tenant_id,name,policy | PK,policy idx | brains-and-sources docs | explicit ACL model |
| sources | Repo partitioning | source_id,tenant_id,config,archived | PK,(tenant_id,source_id),repo expression idx | `sources` table | required source policy metadata |
| pages | Canonical memory unit | page_id,source_id,slug,type,title,content,frontmatter,generation,deleted_at | unique(source_id,slug),type,date,deleted partial | `pages` schema | immutable content revision table |
| page_revisions | Replay/history | rev_id,page_id,hash,author,timestamp | (page_id,timestamp),hash | migration-driven evolution | first-class event sourcing |
| chunks | Retrieval atoms | chunk_id,page_id,chunk_index,text,embedding columns,modality | unique(page_id,chunk_index),hnsw cols,modality partial | `content_chunks` | deterministic chunk lineage |
| links | Graph edges | from_id,to_id,type,source,origin_page,origin_field,resolution_type | from,to,source,origin indexes | `links` schema | edge confidence + evidence refs |
| tags | Labels | page_id,tag | unique(page_id,tag),tag idx | `tags` | tag provenance |
| facts | Structured claims | fact_id,page_id,entity_slug,kind,value,unit,period,confidence,status | entity/time/status indexes | `facts/*`, tests | explicit evidence pointer table |
| takes | Attributed assertions | take_id,page_id,row_num,kind,holder,weight,resolution fields | page/holder/kind indexes | `engine.ts` types | calibration feedback loop |
| timeline_events | Temporal facts | page_id,event_type,date,source,summary,detail | page/date,source/date | timeline inputs | bitemporal validity |
| files | Binary metadata | file_id,source_id,page_id,path,hash,mime,size | unique(source,path),hash idx | engine file types | CAS-backed attachments |
| jobs | async orchestration | job_id,name,status,queue,priority,locks,result,error | claim/status/delay indexes | migrations 5-7 | simpler bounded worker model |
| audits | append-only operational logs | audit_id,kind,timestamp,payload | kind/time | `audit-writer.ts` | tamper-evident hash chain |
| query_cache | retrieval cache | key,source scope,page gens,ttl,payload | key unique,expiry | search cache modules | deterministic invalidation receipts |

## Design caution
Avoid carrying migration debt indefinitely. DuckMemory should:
1. define snapshot baseline migrations,
2. periodically compact migration history,
3. keep formal compatibility tests for upgrade from N-2 baselines.
