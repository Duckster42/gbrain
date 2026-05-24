# GBrain Security and Runtime Review

## Trust boundary evidence
- Architectural docs: `AGENTS.md`, `CLAUDE.md` (remote/local caller distinction).
- Code: `src/core/operations.ts` validator and context comments, MCP dispatch/transport files.
- Tests: `test/destructive-guard.test.ts`, `test/operation-context-sourceid-required.test.ts`, `test/check-system-of-record.test.ts`.

## File/path controls
`validateUploadPath`, `validatePageSlug`, `validateFilename` in `operations.ts` implement path and input restrictions including strict mode for remote paths and deny patterns for dangerous filename/slug constructions.

## Scope controls
`AuthInfo` in `operations.ts` includes client/scopes/source restrictions and federated read allowances. This is a concrete mechanism for source-level access control.

## Runtime assumptions
- Local default engine can be embedded (`pglite`) or external postgres.
- Full CI in docs references Docker and security tools.
- Skillpack/minion surfaces introduce additional execution pathways needing guardrails.

## Security strengths
- explicit trust-context model,
- operation-level validation,
- source-aware scoping,
- audit log hooks,
- separate local-only/admin operation classification.

## Security risks / baggage
- multiple transport modes increase chance of inconsistent context propagation,
- shell/minion orchestration requires strict protected-name and redaction paths,
- broad script surface may conceal unsafe defaults if governance weakens.

## DuckMemory security model recommendations
1. hard fail if trust context absent.
2. immutable operation capability map signed at boot.
3. separate binary/service for privileged operations.
4. mandatory audit entry for every privilege boundary crossing.
5. default remote mode: read-only until explicit grants.
