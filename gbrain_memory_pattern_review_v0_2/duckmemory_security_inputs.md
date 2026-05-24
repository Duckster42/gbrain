# DuckMemory Security Inputs

Requirements:
- no hidden writes,
- approval-aware privileged writes,
- secret blocking by default,
- strict path controls,
- no automatic external service activation,
- audit log for all privileged boundaries,
- sandbox rules for any shell-like task.

Evidence baseline:
- GBrain validators and trust-boundary patterns in `operations.ts` + MCP transport files.
