# DuckMemory Patterns to Reject or Replace

## Replace: broad markdown-only resolver as primary control plane
- GBrain evidence: large trigger matrix in `skills/RESOLVER.md`.
- DuckMemory replacement: typed workflow registry compiled from markdown playbooks.

## Replace: sprawling script surface
- GBrain evidence: dozens of scripts under `scripts/` for checks and orchestration.
- Replacement: typed task runner with immutable task manifest.

## Replace: excessive runtime mode sprawl where unnecessary
- GBrain evidence: multiple deployment patterns and optional providers.
- Replacement: opinionated default local stack with optional adapters.

## Reject: any trust-context ambiguity
- GBrain history/docs emphasize this bug class.
- Replacement: hard fail when trust context missing, plus integration tests.

## Replace: migration chain growth without compaction policy
- GBrain mature chain is valuable but heavy.
- Replacement: periodic baseline snapshots + compatibility importers.

Each rejection includes either a superior replacement or operational simplification justified for Duckster stack maintainability.
