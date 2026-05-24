# Next Stage Recommendation

## Stage 1 (immediate)
Produce DuckMemory v0 clean-room architecture spec with:
- canonical operation schema,
- minimal storage engine contract,
- retrieval stage contract + explain ledger,
- consolidation DAG + provenance/event model.

## Stage 2
Build thin vertical slice:
- ingest 500 docs,
- run hybrid retrieval,
- run graph boosts,
- emit explain output,
- run parity eval set against GBrain-behavior targets.

## Stage 3
Close gaps identified in parity matrix and freeze v1 behavior contracts before scale-out.

## Acceptance gate
Do not accept DuckMemory until measured parity/exceedance on retrieval quality, routing correctness, consolidation behavior, and safety controls.
