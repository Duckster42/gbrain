# 13 Scripts Jobs Map

## Build/schema
Evidence:
- `scripts/build-schema.sh`, `build-llms.ts`, `build-admin-embedded.ts`.
Purpose: generate embedded/schema/docs artifacts.
Risk: stale generated outputs.
DuckMemory eq: typed generator with checksum lock.

## Test orchestration
Evidence:
- `scripts/run-unit-parallel.sh`, `run-e2e.sh`, `run-heavy.sh`, `ci-local.sh`.
Purpose: CI matrix and local automation.
Risk: environment-specific failures.

## Privacy/security checks
Evidence:
- `scripts/check-privacy.sh`, `check-no-pii-in-agent-voice.sh`, `check-source-config-leak.sh`.
Purpose: prevent sensitive leakage.
Risk: false negatives if patterns lag.

## Smoke scripts
Evidence:
- `scripts/smoke-test.sh`, `smoke-test-mcp.ts`, `chunker-smoketest.ts`.

## Jobs/background
Evidence:
- `src/core/minions/queue.ts`, `supervisor.ts`, `worker.ts`, handlers in `src/core/minions/handlers/*`.
Purpose: async task processing, subagents, shell jobs.
Risk: privilege boundary and operational complexity.
DuckMemory eq: minimal bounded job runner with no shell in V0.
