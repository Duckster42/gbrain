# GBrain Skills and Workflow Review

## Evidence corpus
- Dispatcher: `skills/RESOLVER.md`
- Skill protocols: `skills/*/SKILL.md`
- Conventions: `skills/conventions/*.md`
- Skillpack docs: `docs/GBRAIN_SKILLPACK.md`, `docs/skillpack-anatomy.md`, `docs/guides/skill-development.md`
- Skillpack runtime code: `src/core/skillpack/*`

## Resolver behavior
`skills/RESOLVER.md` maps user intents to specific skill files and includes always-on routing rules (`signal-detector`, `brain-ops`) plus disambiguation hierarchy. This is an explicit policy router.

## Workflow categories encoded
- ingestion (capture, idea-ingest, media-ingest, meeting-ingestion),
- query/enrich,
- maintenance/consolidation,
- scheduling/minions,
- migration/setup,
- quality/citation/frontmatter checks,
- schema authoring.

## Read-before-action/write-after-action conventions
- `skills/conventions/brain-first.md`: prioritize brain lookup before external research.
- `skills/conventions/brain-routing.md`: force explicit brain/source choice logic.
- `skills/conventions/quality.md`: citation and output quality constraints.

## Risks
- policy drift: markdown docs can diverge from code reality.
- resolver breadth: large trigger table increases overlap/conflict.
- maintenance burden: every skill revision is manual policy maintenance.

## DuckMemory replacement strategy
- Keep human-readable playbooks but compile to typed workflow descriptors.
- Add schema validation for each workflow step (required inputs, allowed operations, expected outputs).
- Add automated “policy-to-runtime parity tests” ensuring workflow references valid operations.
- Version workflow bundles and track compatibility with operation contract versions.
