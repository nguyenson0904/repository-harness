# Agent Instructions

This repository uses a lightweight Markdown-only agent harness.

Before changing code or product docs, read:

- `README.md`
- `docs/WORKFLOW.md`
- `docs/FEATURE_INTAKE.md`
- `docs/CONTEXT_RULES.md`
- `docs/CODING_RULES.md`

When the work touches architecture, API shape, database, boundaries, providers,
or cross-module behavior, also read:

- `docs/ARCHITECTURE.md`
- Relevant files under `docs/product/`
- Relevant files under `docs/stories/`
- Relevant files under `docs/decisions/`

## Operating Rules

- Classify every request as `tiny`, `normal`, or `high-risk` before editing.
- Keep product truth in `docs/product/`.
- Keep implementation slices in `docs/stories/`.
- Keep durable decisions in `docs/decisions/`.
- Use Markdown checklists for status and validation. This lite harness has no
  CLI, database, matrix, codegen, or hidden state.
- After implementation, update the related story with status, validation run,
  files changed, and follow-ups.
- If a rule, template, or product doc was missing and caused friction, update
  the docs directly or add a follow-up to `docs/stories/backlog.md`.

## Done Definition

A task is done only when:

- The requested change is completed or the blocker is documented.
- The related product docs and story are current.
- Available validation commands were run, or the reason they were not run is
  recorded.
- Any architecture/product decision that should outlive the task is captured in
  `docs/decisions/`.
- The final response states what changed, what was validated, and what was not
  attempted.
