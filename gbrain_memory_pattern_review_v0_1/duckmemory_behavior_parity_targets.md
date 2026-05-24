# DuckMemory Behavior Parity Targets

## Target 1: Routing correctness
- Requirement: brain/source precedence equivalent to GBrain routing docs.
- Acceptance test: 30-case matrix across explicit flag/env/dotfile/path/default; all expected routes match.

## Target 2: Retrieval quality parity
- Requirement: hybrid lexical+vector+post-fusion pipeline.
- Acceptance test: frozen 200-query corpus; NDCG@10 within ±2% of GBrain baseline and no severe regressions on high-priority queries.

## Target 3: Explainability parity
- Requirement: per-result stage attribution fields.
- Acceptance test: explain snapshots validate stage list, factors, and final score derivation for canonical fixtures.

## Target 4: Graph signal parity
- Requirement: adjacency and cross-source graph signals integrated post-fusion.
- Acceptance test: graph-signal fixtures verify expected reorder and floor-gate behavior.

## Target 5: Facts/takes parity
- Requirement: typed fact extraction and take resolution states.
- Acceptance test: fixture set verifies schema-conform extraction and resolution transitions.

## Target 6: Consolidation parity
- Requirement: idempotent consolidation DAG with replay.
- Acceptance test: run consolidate twice on same snapshot; zero semantic diff on second run.

## Target 7: Security parity-or-better
- Requirement: fail-closed trust context, source-scoped auth, strict path validation.
- Acceptance test: remote calls without trust/scope are denied; traversal/symlink cases rejected.

## Target 8: Cache correctness
- Requirement: generation-aware invalidation and mode-key segregation.
- Acceptance test: update content invalidates cached results; mode change never cross-serves cache entries.

## Target 9: Auditability
- Requirement: append-only audit records for security-sensitive and failure events.
- Acceptance test: synthetic failure scenario emits complete audit chain with request id correlation.

## Target 10: Eval gate discipline
- Requirement: release blocked when key retrieval/consolidation/security metrics regress.
- Acceptance test: CI pipeline enforces gates with machine-readable report artifacts.
