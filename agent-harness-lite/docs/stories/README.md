# Stories

Stories are implementation-sized slices of product work.

Create a story when work is larger than a tiny edit:

```text
docs/stories/US-001-order-list.md
docs/stories/US-002-create-order.md
```

Use `docs/templates/story.md`.

## Status Values

| Status | Meaning |
| --- | --- |
| planned | Accepted as intended work, not started |
| in_progress | Actively being built |
| implemented | Implemented and validation evidence exists |
| changed | Contract changed after earlier implementation |
| retired | No longer part of the product contract |

## Story Closeout

Before closing a story:

- Update status.
- Check acceptance criteria.
- Record validation run.
- List files changed.
- Add follow-ups or decisions when needed.
