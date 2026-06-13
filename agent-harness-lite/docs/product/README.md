# Product Docs

Product docs are the living product contract.

Put feature source material here before implementation:

```text
docs/product/features/<feature-name>/
  README.md
  po.md
  erd.md
  screens.md
  assets/
```

Recommended files:

- `README.md`: feature summary, scope, links, open questions.
- `po.md`: PO document, goals, business rules, acceptance notes.
- `erd.md`: database model, ownership, relationships, constraints.
- `screens.md`: screen list, UI components, fields, states, interactions.
- `assets/`: diagrams, screenshots, wireframes.

Do not treat a large one-time spec as the permanent operating manual. Break it
into smaller product docs, stories, and decisions as work becomes accepted.

## Feature README Template

```md
# <Feature Name>

## Summary

## In Scope

## Out Of Scope

## Source Documents

- `po.md`
- `erd.md`
- `screens.md`

## Open Questions
```
