# Feature Intake

Every implementation prompt enters intake before code changes. The human does
not need to classify risk; the agent does.

## Intake Flow

```text
User prompt
  -> classify input type
  -> restate as work item
  -> find affected product docs and stories
  -> run risk checklist
  -> choose lane: tiny, normal, or high-risk
```

## Input Types

| Type | Use when | Typical artifact |
| --- | --- | --- |
| New spec | Turning a supplied product spec into repo-ready docs | Product docs, candidate stories, decisions |
| Spec slice | Implementing selected behavior from accepted docs | Story |
| Change request | Changing, fixing, or refining accepted behavior | Story or direct patch |
| New initiative | Adding a larger product area that needs multiple stories | Feature folder and stories |
| Maintenance request | Dependency, architecture, performance, security, or operational work | Story, validation notes, or decision |
| Harness improvement | Improving the agent workflow itself | Docs/template update or backlog item |

## Lanes

### Tiny

Use for low-risk docs, copy, names, narrow config edits, or very small code
changes with no contract change.

Requirements:

- Patch directly.
- Keep affected docs current.
- Run available quick checks when relevant.
- Update backlog only if friction was found.

### Normal

Use for story-sized behavior with bounded blast radius.

Requirements:

- Create or update one story from `docs/templates/story.md`.
- Link relevant product docs.
- Implement the smallest vertical slice.
- Update validation checklist and status in the story.

### High-Risk

Use when the work can affect security, data, scope, contracts, or multiple
roles/platforms.

Requirements:

- Create or update a story with stronger design and validation notes.
- Read relevant decisions before implementation.
- Ask for human confirmation if direction is ambiguous.
- Create a decision record when behavior, architecture, data ownership, API
  shape, auth, security, or validation requirements change meaningfully.

## Risk Checklist

Mark each flag that applies:

| Risk flag | Applies when the work touches |
| --- | --- |
| Auth | login, logout, sessions, JWT, password, refresh token |
| Authorization | roles, permissions, tenant or organization scope |
| Data model | schema, migrations, uniqueness, deletion, retention |
| Audit/security | audit logs, privacy, sensitive data, access logs |
| External systems | email, payments, cloud services, provider SDKs, queues, webhooks |
| Public contracts | API shape, response envelope, client-visible behavior |
| Cross-platform | browser/mobile/desktop split, native shell behavior, deep links |
| Existing behavior | implemented or test-covered behavior changes |
| Weak proof | unclear or missing checks around the affected area |
| Multi-domain | more than one product domain changes at once |

## Classification

```text
0-1 flags:
  tiny or normal, based on code impact

2-3 flags:
  normal with stronger validation

4+ flags:
  high-risk

Any hard gate:
  high-risk unless the human explicitly narrows scope
```

Hard gates:

- Auth.
- Authorization.
- Data loss or migration.
- Audit/security.
- External provider behavior.
- Removing or weakening validation requirements.

## Intake Output

At the end of intake, the agent should be able to say:

```text
Lane: normal
Reason: touches API contract and screen behavior.
Docs: docs/product/features/orders/po.md, docs/product/features/orders/screens.md.
Story: docs/stories/US-001-order-list.md.
Validation: unit + manual screen check.
```
