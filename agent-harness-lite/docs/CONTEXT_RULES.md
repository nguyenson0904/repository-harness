# Context Rules

Context rules tell agents what to read and when to stop reading. The goal is
not maximum context; the goal is the right context for the current phase.

## Always Read First

For every task:

- `AGENTS.md`
- `README.md`
- `docs/WORKFLOW.md`
- `docs/FEATURE_INTAKE.md`
- `docs/CONTEXT_RULES.md`

## Intake Phase

Read to classify the request and find the affected surface.

| Source | Tiny | Normal | High-risk |
| --- | --- | --- | --- |
| `docs/product/*` | If directly related | Must | Must |
| `docs/stories/*` | If story exists | Must if story exists | Must |
| `docs/ARCHITECTURE.md` | Skip unless structural | Should | Must |
| `docs/decisions/*` | Skip unless relevant | Should if architecture/data/API touched | Must |

## Planning Phase

Read to decide the smallest safe approach and expected proof.

| Source | Tiny | Normal | High-risk |
| --- | --- | --- | --- |
| Files to edit | Must | Must | Must |
| Adjacent files with same pattern | Should | Must | Must |
| `docs/templates/story.md` | Skip | Must when creating/updating story | Must |
| Relevant product docs | Should if behavior changes | Must | Must |
| Relevant decisions | Skip unless touched | Should | Must |

## Implementation Phase

Keep implementation context scoped to:

- files being changed,
- adjacent patterns,
- related product docs,
- related story,
- architecture docs if structure/boundaries change.

Do not read unrelated historical docs after the lane, affected files, and
validation path are clear.

## Validation Phase

Before claiming completion, read:

- story acceptance criteria,
- story validation checklist,
- available test/build commands from project docs,
- validation report template if proof is notable or high-risk.

## Closeout Phase

Before final response:

- Re-read changed story or product docs.
- Check changed files.
- Update validation notes and follow-ups.
- Add decisions/backlog items if the task changed durable truth or revealed
  friction.

## Retrieval Triggers

| Trigger | Action |
| --- | --- |
| Task touches database schema or data ownership | Read `docs/ARCHITECTURE.md`, product ERD, and relevant decisions |
| Task changes API shape or client-visible behavior | Read product docs, screen docs, and relevant stories |
| Task touches auth, authorization, audit/security, data loss, or provider behavior | Treat as high-risk |
| Task changes source-of-truth or validation policy | Read workflow, intake, architecture, and decisions before editing |
| Task reveals repeated confusion or missing docs | Update docs directly or add a backlog item |
