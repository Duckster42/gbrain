# DuckMemory GBrain Parity Matrix (35+ rows)

| GBrain Capability | GBrain Evidence | Implementation Notes | Why It Matters | DuckMemory Equivalent | Match / Exceed / Replace | Acceptance Test | Risk If Missed | Status |
|---|---|---|---|---|---|---|---|---|
| Operation contract model | `src/core/operations.ts` | central typed operation registry | consistency | unified contracts | Match | CLI/API call same op id returns same shape | drift | Planned |
| Engine abstraction | `src/core/engine.ts` | backend interface | portability | storage interface | Match | same retrieval tests pass on 2 backends | lock-in | Planned |
| Engine factory | `engine-factory.ts` | runtime backend selector | deploy flexibility | adapter loader | Replace | no handler branching | complexity | Planned |
| Brain routing | architecture docs | db boundary | isolation | tenant router | Match | precedence matrix tests | leakage | Planned |
| Source routing | brain-routing convention + tests | corpus scope | relevance & ACL | source router | Match | scope tests pass | wrong answers | Planned |
| Pages | schema pages table | canonical memory unit | base entity | pages+revisions | Exceed | revision audit diff exists | provenance loss | Planned |
| Chunks | content_chunks | retrieval granularity | recall | chunks | Match | deterministic chunk rebuild | recall drop | Planned |
| Facts | facts modules/tests | structured claims | reasoning substrate | facts table | Match | extraction fixtures pass | unstructured sprawl | Planned |
| Takes | engine types/tests | attributed assertions | uncertainty modeling | takes table | Match | resolution state tests | no calibration | Planned |
| Links | links schema | graph edges | relationships | edges | Match | dedup+provenance tests | graph corruption | Planned |
| Tags | tags table | facets | filtering | tags | Match | tag query tests | discoverability loss | Planned |
| Timeline | timeline fields/types | temporal context | chronology | events table | Exceed | bitemporal tests | temporal errors | Planned |
| Files metadata | files types/schema/migrations | multimodal refs | asset traceability | files table | Match | hash/path uniqueness tests | orphaned assets | Planned |
| Audit logs | audit writer modules | forensics | trust/ops | append-only audit | Exceed | failure emits audit record | blind incidents | Planned |
| Jobs queue | minion tables/code | async automation | throughput | bounded jobs | Replace | queue lifecycle tests | instability | Planned |
| Hybrid retrieval | `search/hybrid.ts` | stage pipeline | quality | hybrid engine | Match | ranking fixture parity | weak answers | Planned |
| Vector retrieval | `search/vector.ts` | semantic recall | long-tail match | vector stage | Match | semantic benchmark | misses | Planned |
| Lexical retrieval | `search/keyword.ts` | precision | exactness | lexical stage | Match | exact-term benchmark | noise | Planned |
| Fusion/rerank | hybrid + rerank modules | combine signals | robustness | fusion stack | Match | order snapshot tests | unstable rank | Planned |
| Graph boost | graph-signals module | adjacency/cross-source | structural relevance | graph stage | Match | graph reorder fixtures | context loss | Planned |
| Explain ledger | explain formatter | per-stage transparency | debug/trust | explain API | Match | explain snapshot tests | black box | Planned |
| Query cache | query-cache module | latency cost | efficiency | cache layer | Match | cache hit+correctness tests | cost spike | Planned |
| Cache invalidation | generation trigger + gate | staleness control | correctness | generation gate | Match | update invalidates cache | stale results | Planned |
| Schema migrations | migrate registry | upgrade durability | operability | migration engine | Match | migration replay tests | upgrade failure | Planned |
| Consolidation | cycle consolidate phase | entropy control | memory quality | consolidation DAG | Match | idempotence test | drift | Planned |
| Citation repair | citation-fixer skill | source integrity | anti-hallucination | citation model | Exceed | broken citation fix tests | low trust | Planned |
| Entity enrichment | enrich/facts modules | richer nodes | usefulness | enrichment DAG | Match | enrichment fixture tests | shallow memory | Planned |
| Fact extraction | facts extract modules | typed facts | downstream analytics | fact extractor | Match | schema-conform extraction tests | weak structure | Planned |
| Take extraction | extract-takes | uncertainty capture | decision support | take extractor | Match | holder/weight parse tests | false certainty | Planned |
| Skills resolver | `skills/RESOLVER.md` | intent routing | workflow consistency | typed workflow registry | Replace | resolver mapping tests | workflow drift | Planned |
| CLI/MCP shared ops | cli + mcp + ops | transport parity | predictable behavior | shared adapters | Match | same op across transports | divergence | Planned |
| Remote trust boundary | docs + mcp transport + ops ctx | privilege safety | security | fail-closed context | Exceed | missing ctx denied | vuln | Planned |
| Path/file controls | validators in ops | fs safety | prevent traversal | path policy | Match | traversal tests | data exfil | Planned |
| Privacy controls | scripts + tests | pii prevention | compliance | privacy gates | Match | pii scanners in CI | leakage | Planned |
| Tests/evals | large test tree + eval docs | regression control | stability | eval harness | Match | release gate on regressions | silent decay | Planned |
| Observability | telemetry/audit modules | diagnose quality | ops | traces+audits | Exceed | correlated trace IDs | opaque failures | Planned |
| Background maintenance | cycle/minions/docs | upkeep | long-term quality | scheduled DAGs | Replace | deterministic maintenance run tests | entropy | Planned |
| Docs/code parity | docs claims map | trustworthiness | onboarding | generated docs | Exceed | docs parity lint | stale docs | Planned |
