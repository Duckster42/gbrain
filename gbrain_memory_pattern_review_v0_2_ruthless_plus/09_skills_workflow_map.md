# 09 Skills Workflow Map

Evidence:
- `skills/RESOLVER.md`
- `skills/conventions/brain-routing.md`, `brain-first.md`, `quality.md`
- `skills/maintain/SKILL.md`, `query/SKILL.md`, `enrich/SKILL.md`
- runtime support code: `src/core/skillpack/*`

Structure:
- dispatcher maps intents to skill files.
- conventions act as cross-skill policy.
- many domain/task skills encode procedural runbooks.

Read-before-action/write-after-action:
- brain-first convention demands lookup before external research.
- routing convention requires explicit brain/source decisions.

Risks:
- policy drift between markdown and runtime operations.

DuckMemory approach:
- keep readable runbooks,
- compile to typed workflow contracts,
- add parity tests ensuring each workflow step maps to valid operations.
