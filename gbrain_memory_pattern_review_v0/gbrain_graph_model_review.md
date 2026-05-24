# GBrain Graph Model Review
- Primary graph table: links with provenance (`link_source`, `origin_page_id`, `origin_field`).
- Graph traversal supports source scoping and frontier caps.
- Graph is used both for user-facing query ops and ranking-stage boosts.
- Strength: provenance-rich edges enable repair and explainability.
- Replaceable baggage: do not tie graph health to opaque background side effects; use explicit graph materialization jobs with idempotent checkpoints.
