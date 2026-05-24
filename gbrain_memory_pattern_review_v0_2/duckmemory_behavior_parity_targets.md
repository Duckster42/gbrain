# DuckMemory Behavior Parity Targets

1. V0 behavior: two-axis routing.
- GBrain evidence: brains-and-sources docs + source resolver tests.
- Acceptance test: precedence matrix pass.
- Exceed target: policy engine prevents ambiguous writes.

2. V0 behavior: hybrid retrieval with explain.
- Evidence: `search/hybrid.ts`, `explain-formatter.ts`, search tests.
- Acceptance: explain snapshot parity.
- Exceed: deterministic replay mode.

3. V0 behavior: source-scoped security.
- Evidence: `AuthInfo` source fields + oauth scope tests.
- Acceptance: unauthorized source denied.
- Exceed: capability manifests with cryptographic signatures.

4. V0 behavior: consolidation idempotence.
- Evidence: consolidate phase + cycle tests.
- Acceptance: second run no semantic diff.
- Exceed: consolidation receipts with transform hashes.

5. V0 behavior: cache correctness.
- Evidence: generation trigger + cache gate.
- Acceptance: content update invalidates cache.
- Exceed: cache proof records embedded in explain.
