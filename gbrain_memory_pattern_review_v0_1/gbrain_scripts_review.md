# GBrain Scripts Review

## Script categories with evidence

### Build/generation
- `scripts/build-schema.sh`
- `scripts/build-llms.ts`
- `scripts/build-admin-embedded.ts`
- `scripts/build-skillpack-anatomy.ts`
- `scripts/generate-gbrain-base.ts`
- `scripts/generate-metric-glossary.ts`

Purpose: generate embedded assets, docs maps, schema/materialized references.
Risk: generation drift if outputs not pinned in CI.

### Test orchestration
- `scripts/run-unit-parallel.sh`
- `scripts/run-unit-shard.sh`
- `scripts/run-serial-tests.sh`
- `scripts/run-e2e.sh`
- `scripts/run-heavy.sh`
- `scripts/run-slow-tests.sh`
- `scripts/test-shard.sh`
- `scripts/select-e2e.ts`

Purpose: scale test execution across categories.
Risk: environment coupling and partial-run confusion.

### Smoke checks
- `scripts/smoke-test.sh`
- `scripts/smoke-test-mcp.ts`
- `scripts/chunker-smoketest.ts`
- `scripts/image-decoders-smoketest.ts`

### Security/privacy/compliance checks
- `scripts/check-privacy.sh`
- `scripts/check-test-real-names.sh`
- `scripts/check-no-pii-in-agent-voice.sh`
- `scripts/check-pg-url-redaction.sh`
- `scripts/check-source-config-leak.sh`
- `scripts/check-test-isolation.sh`
- `scripts/check-synthetic-corpus-privacy.sh`

### Structural/consistency checks
- `scripts/check-system-of-record.sh`
- `scripts/check-admin-scope-drift.sh`
- `scripts/check-source-id-projection.sh`
- `scripts/check-jsonb-pattern.sh`
- `scripts/check-no-legacy-getconnection.sh`
- `scripts/check-exports-count.sh`

### CI envelope
- `scripts/ci-local.sh`
- profiling helpers (`scripts/profile-tests.sh`)

## Side-effect considerations
These scripts primarily orchestrate checks/builds; some imply runtime dependencies (docker, binaries). For DuckMemory, replace ad hoc shell spread with one typed task runner and immutable task registry.

## DuckMemory replacement plan
1. `tasks.yaml` manifest for all checks/builds.
2. one entrypoint CLI: `duckmem task <name>`.
3. category-level policy: build/test/security/release.
4. machine-readable output contracts for CI aggregation.
