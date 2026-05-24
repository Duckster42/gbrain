# 07 Enrichment and Extraction Map

Evidence:
- `src/core/facts/extract.ts`, `extract-from-fence.ts`, `facts/extract.ts`
- `src/core/cycle/extract-facts.ts`, `extract-takes.ts`
- `src/core/think/entity-extract.ts`
- docs: `docs/guides/enrichment-pipeline.md`, `docs/takes-vs-facts.md`
- tests: `test/facts-extract.test.ts`, `test/facts-classify.test.ts`, `test/extract-takes-holder-producer-seam.test.ts`

Capability map:
- Entity extraction: keep (DuckMemory local NER + rule pipeline).
- Fact extraction: keep with typed schema.
- Take extraction: keep with holder/weight/status semantics.
- Citation/source attachment: replace with explicit citation table and hash anchors.
- External enrich assumptions: replace with provider-optional adapters.
- Failure/audit behavior: keep via append-only audits (`audit-writer.ts`, `facts/phantom-audit.ts`).

Evidence gap:
- Missing evidence: single canonical external enrichment contract.
- Why it matters: provider portability risk.
- DuckMemory assumption needed: adapter interface with deterministic fallback.
