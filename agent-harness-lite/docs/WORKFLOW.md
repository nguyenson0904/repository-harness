# Workflow

This harness is intentionally Markdown-only. Policy lives in docs. Progress
lives in story files. Decisions live in decision records.

## Work Loop

```text
User prompt
  -> classify input type and lane
  -> locate relevant product docs
  -> create or update a story when needed
  -> plan the smallest safe implementation
  -> implement
  -> validate
  -> update story status and evidence
  -> update product docs, decisions, or backlog if needed
  -> final response
```

## Source Hierarchy

```text
User prompt or supplied spec
  input material for new work

docs/product/*
  living product contract

docs/stories/*
  implementation slices, progress, validation notes, follow-ups

docs/decisions/*
  durable architecture, data, API, security, or process decisions
```

Before implementation, product docs describe intent. After implementation,
product docs plus executable checks become the living contract.

## Task Outputs

Every task may create two kinds of output:

- Product delta: source code, tests, config, API shape, data model, UI, or
  product docs.
- Harness delta: story updates, decision records, validation notes, backlog
  items, or template/process clarifications.

## Story Rules

Use a story when work is larger than a tiny edit.

Create stories from `docs/templates/story.md` and place them under
`docs/stories/`.

A story should include:

- goal,
- product docs linked,
- acceptance criteria,
- implementation notes,
- validation checklist,
- status,
- files changed,
- follow-ups.

## Decision Rules

Create a decision record from `docs/templates/decision.md` when a task changes:

- architecture direction,
- database ownership or schema strategy,
- public API shape,
- auth or authorization rules,
- audit/security behavior,
- validation requirements,
- source-of-truth hierarchy.

## Closeout Checklist

Before final response:

- Update the story status and validation notes.
- Update product docs if the contract changed.
- Add a decision record if a durable decision was made.
- Add backlog follow-ups if something important remains.
- State validation run and any validation not run.
