# GBrain Enrichment Pipeline Review
- Entity/fact extraction appears split across cycle + facts modules.
- Supports typed claims, trajectory extraction, and signal scoring.
- Uses audits for fallback/failure visibility.
- Strength: enrichment is not just extraction; includes reconciliation and evidence-aware updates.
- DuckMemory recommendation: implement enrichment as DAG with replayable artifacts and immutable extraction traces.
