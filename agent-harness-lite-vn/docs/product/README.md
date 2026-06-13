# Product Docs

Product docs là living product contract.

Đặt source material của feature ở đây trước khi implement:

```text
docs/product/features/<feature-name>/
  README.md
  po.md
  erd.md
  screens.md
  assets/
```

Các file khuyến nghị:

- `README.md`: tóm tắt feature, scope, links, open questions.
- `po.md`: PO document, goals, business rules, acceptance notes.
- `erd.md`: database model, ownership, relationships, constraints.
- `screens.md`: screen list, UI components, fields, states, interactions.
- `assets/`: diagrams, screenshots, wireframes.

Đừng xem một spec lớn dùng một lần là operating manual vĩnh viễn. Hãy tách nó
thành product docs nhỏ hơn, stories, và decisions khi work được chấp nhận.

## Feature README Template

```md
# <Tên Feature>

## Summary

## In Scope

## Out Of Scope

## Source Documents

- `po.md`
- `erd.md`
- `screens.md`

## Open Questions
```
