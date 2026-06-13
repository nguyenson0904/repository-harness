# Agent Harness Lite

`agent-harness-lite` is a small Markdown-only project harness for coding
agents.

It keeps the useful parts of a repository harness:

- a stable agent entrypoint,
- a simple work classification step,
- product documentation as living contract,
- story-sized implementation packets,
- decision records,
- validation checklists,
- follow-up/backlog capture.

It deliberately excludes:

- CLI tooling,
- SQLite or any durable database,
- test matrix commands,
- code generation,
- release workflows,
- language-specific scaffolding,
- application source code.

The goal is to make a repo easier for AI coding agents to work in without
making the process hard to understand.

## Folder Layout

```text
.
  AGENTS.md
  README.md
  docs/
    WORKFLOW.md
    FEATURE_INTAKE.md
    CONTEXT_RULES.md
    ARCHITECTURE.md
    product/
    stories/
    decisions/
    templates/
```

## Typical Flow

```text
user intent
  -> classify lane
  -> locate product docs
  -> create or update story
  -> implement
  -> run validation
  -> update story checklist
  -> capture decisions or follow-ups
  -> final response
```

## Where To Put Feature Documents

For a new feature, put source material under:

```text
docs/product/features/<feature-name>/
  README.md
  po.md
  erd.md
  screens.md
  assets/
```

Then create implementation stories under:

```text
docs/stories/US-001-<short-name>.md
```

Stories should link back to the product docs they implement.
