# DuckMemory Graph Inputs

Entity types:
- page nodes typed by domain schema (person/company/project/system/etc).

Edge types:
- link_type taxonomy + relation confidence.

Provenance:
- extraction source, origin page/field, evidence references.

Supersession/timeline:
- superseded edges/facts remain queryable in history mode.

Project boundaries:
- source/tenant constraints enforced on traversal/ranking.

Acceptance:
- provenance retention after extraction rebuild,
- scoped traversal tests,
- graph-signal ranking guardrail tests.
