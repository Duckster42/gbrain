# GBrain Memory Layout Review
- Two-axis routing: Brain (database) + Source (repo-in-db).
- Storage domains:
  - pages (core markdown/code/image entities),
  - content_chunks (vectorized retrieval substrate),
  - links/timeline/tags/facts/takes (semantic overlays),
  - files (binary metadata),
  - job/audit/oauth tables (operations plane).
- Practical impact: supports mixed personal/team knowledge topologies and source-scoped isolation.
- DuckMemory parity requirement: preserve orthogonal routing axes, source-aware slugs, and soft-delete lifecycle.
