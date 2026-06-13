# Coding Rules

Use this file for project-specific coding conventions that agents must follow
on every code change.

These are sample rules. Adjust them to match the real project.

## Naming

- Entity, class, type, interface, enum, database table, column, API field, and
  event names must be written in English.
- Do not name domain concepts or entities in Vietnamese inside source code.
- Local variable names should also be English unless the value is explicitly a
  user-facing localized text key or fixture.
- Use consistent domain names across product docs, code, database, and API.

Good:

```text
Customer
OrderItem
PaymentStatus
created_at
```

Avoid:

```text
KhachHang
DonHang
TrangThaiThanhToan
ngay_tao
```

## Code Comments

- Code comments should be written in Vietnamese with accents.
- Add comments only when they explain business intent, a non-obvious tradeoff,
  or an edge case that code alone does not make clear.
- Do not add comments that merely restate what the next line of code does.
- Keep public API docs in the language expected by the project or consumers. If
  there is no consumer requirement, prefer English for public API docs and
  Vietnamese for internal implementation comments.

Good:

```text
// Giữ trạng thái cũ để tránh mất dữ liệu khi provider trả về timeout.
```

Avoid:

```text
// Set status to pending.
```

## Localization

- Do not hardcode Vietnamese UI text in source code.
- All user-facing text must go through the project's localization function,
  translation file, or message catalog.
- When adding a new UI string, add the corresponding localization key and
  translation entry.
- Do not concatenate localized text from fragments if grammar may change by
  language. Prefer full sentence keys with interpolation placeholders.
- Exceptions are allowed for tests, mocks, debug-only logs, or seed data only
  when the text cannot appear in production UI.

Example pattern:

```text
t("orders.create.success")
```

Avoid:

```text
"Tạo đơn hàng thành công"
```

## Errors And Logs

- User-visible errors must be localized.
- Developer logs may be English or Vietnamese, but should be consistent within
  the project.
- Logs must not include secrets, tokens, passwords, or personal data unless the
  product explicitly defines a safe audit policy.

## Tests

- Test names should describe behavior in English unless the existing test suite
  uses another convention.
- Test fixtures may contain Vietnamese text when testing localization,
  rendering, search, encoding, or product examples.
- If a test adds user-visible text, assert against localization keys or rendered
  localized output according to the project pattern.

## Review Checklist

Before closing a task, check:

- [ ] New entity/domain names are English.
- [ ] Database/API fields are English and consistent with product docs.
- [ ] Code comments follow the project comment language rule.
- [ ] No Vietnamese UI text is hardcoded in production code.
- [ ] New user-facing text goes through localization.
- [ ] Exceptions are documented in the story or implementation notes.
