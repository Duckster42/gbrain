# GBrain Retrieval/Search Review
- Hybrid pipeline: keyword + vector + post-fusion stages (backlink, salience, recency, exact-match, graph signals).
- Query modes (`conservative/balanced/tokenmax`) + knob hashing + cache partitioning.
- Explain formatter gives per-result score contributions.
- Strong anti-regression posture through audit and eval modules.
- DuckMemory parity target: identical explain surface with deterministic stage attribution and explicit feature flags.
