# RIVET_GBRAIN_MEMORY_PATTERN_REVIEW_V0 — Summary

Static-only autopsy completed across architecture, schema, retrieval, graph, skills, MCP boundary, scripts, tests/evals, and operational assumptions.

## Verdict
- GBrain is a contract-first memory operating system, not just an embedding DB.
- The practical value comes from **interlocking subsystems**: schema+migrations, hybrid retrieval, graph boosts, skill resolver, job queue, and trust boundaries.
- A parity-or-better DuckMemory is feasible if it preserves behavior-level capabilities while replacing high-baggage runtime surfaces (Bun/global install, broad script surface, mixed local/remote trust complexity).

## DuckMemory viability call
DuckMemory can beat GBrain for RIVET/SKYE if it keeps:
1. two-axis routing (brain/source equivalent),
2. retrieval explainability + mode control,
3. graph-aware reranking,
4. durable enrichment/consolidation loops,
5. strict remote trust posture by default,
6. eval gates for regression control.

All required artifacts are in this folder.
