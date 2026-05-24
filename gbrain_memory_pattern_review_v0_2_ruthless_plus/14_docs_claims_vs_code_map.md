# 14 Docs Claims vs Code Map

| Claim | Doc evidence | Code evidence | Status | DuckMemory implication |
|---|---|---|---|---|
| Contract-first operations | `CLAUDE.md` architecture section | `src/core/operations.ts` | Confirmed | keep single contract source |
| Two-axis brain/source routing | `docs/architecture/brains-and-sources.md` | source-scoped schema + resolver/tests | Confirmed | keep orthogonal routing |
| Remote/local trust boundary | `AGENTS.md`, `CLAUDE.md` | `operations.ts` context, MCP transport files | Confirmed | fail-closed trust model |
| Hybrid retrieval + explain | `docs/architecture/RETRIEVAL.md`, `docs/guides/search-modes.md` | `src/core/search/*`, explain tests | Confirmed | must preserve explain ledger |
| Minion orchestration | `docs/designs/MINIONS_AGENT_ORCHESTRATION.md` | `src/core/minions/*`, migrations | Confirmed | replace with narrower V0 job model |
| Eval discipline | `docs/eval/SEARCH_MODE_METHODOLOGY.md` | eval tests/harness files | Confirmed | parity gates mandatory |
| Citation quality conventions | `skills/conventions/quality.md` | citation-fixer skill; partial code hooks | Partial | add explicit citation data model |

Evidence gap:
- Missing evidence: complete docs-to-op map in one canonical file.
- Why it matters: onboarding and auditability.
- DuckMemory assumption needed: auto-generated docs from operation registry.
