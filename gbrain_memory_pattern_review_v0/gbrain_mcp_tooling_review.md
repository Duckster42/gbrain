# GBrain MCP + Tooling Review
- MCP stack includes server, dispatch, transport, tool defs, and rate limits.
- Core design: same operation contract exposed to CLI and remote callers.
- Strength: consistency.
- Risk: remote misuse if trust fields are omitted (historical bug class noted in docs/comments).
- DuckMemory requirement: fail-closed remote context defaults, enforced at compile-time and runtime.
