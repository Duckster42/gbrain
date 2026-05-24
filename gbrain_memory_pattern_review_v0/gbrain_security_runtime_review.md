# GBrain Security + Runtime Assumptions Review
- Explicit local-vs-remote trust boundary is a major positive.
- File upload/path validation and source-scoped auth controls are present.
- Runtime baggage includes Bun/global installation paths and complex multi-mode operations.
- Dependency/runtime assumptions include Docker for full CI path and external DB options.
- DuckMemory replacement direction: minimize privileged operations; separate control plane from data plane; default-deny for remote writes and filesystem reach.
