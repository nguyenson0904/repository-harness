# Feature Intake

Mọi implementation prompt đều đi qua intake trước khi sửa code. Human không cần
tự phân loại rủi ro; agent sẽ làm việc đó.

## Intake Flow

```text
User prompt
  -> phân loại input type
  -> diễn đạt lại thành work item
  -> tìm product docs và stories liên quan
  -> chạy risk checklist
  -> chọn lane: tiny, normal, hoặc high-risk
```

## Input Types

| Type | Dùng khi | Artifact thường tạo |
| --- | --- | --- |
| New spec | Biến spec sản phẩm được cung cấp thành docs sẵn sàng cho repo | Product docs, candidate stories, decisions |
| Spec slice | Implement một hành vi đã được chấp nhận trong docs | Story |
| Change request | Thay đổi, sửa bug, hoặc refine hành vi đã chấp nhận | Story hoặc direct patch |
| New initiative | Thêm một vùng sản phẩm lớn cần nhiều story | Feature folder và stories |
| Maintenance request | Dependency, architecture, performance, security, hoặc operational work | Story, validation notes, hoặc decision |
| Harness improvement | Cải thiện workflow cho human và agent | Docs/template update hoặc backlog item |

## Lanes

### Tiny

Dùng cho docs, copy, tên, config hẹp, hoặc thay đổi code rất nhỏ không đổi
contract.

Yêu cầu:

- Patch trực tiếp.
- Giữ docs liên quan luôn đúng.
- Chạy quick checks khả dụng khi phù hợp.
- Chỉ cập nhật backlog nếu phát hiện friction.

### Normal

Dùng cho behavior cỡ story với blast radius rõ và giới hạn.

Yêu cầu:

- Tạo hoặc cập nhật một story từ `docs/templates/story.md`.
- Link product docs liên quan.
- Implement vertical slice nhỏ nhất.
- Cập nhật validation checklist và status trong story.

### High-Risk

Dùng khi công việc có thể ảnh hưởng security, data, scope, contracts, hoặc
nhiều role/platform.

Yêu cầu:

- Tạo hoặc cập nhật story với design và validation notes rõ hơn.
- Đọc decisions liên quan trước khi implement.
- Hỏi human xác nhận nếu hướng đi còn mơ hồ.
- Tạo decision record khi behavior, architecture, data ownership, API shape,
  auth, security, hoặc validation requirements thay đổi đáng kể.

## Risk Checklist

Đánh dấu mỗi flag phù hợp:

| Risk flag | Áp dụng khi công việc chạm tới |
| --- | --- |
| Auth | login, logout, sessions, JWT, password, refresh token |
| Authorization | roles, permissions, tenant hoặc organization scope |
| Data model | schema, migrations, uniqueness, deletion, retention |
| Audit/security | audit logs, privacy, sensitive data, access logs |
| External systems | email, payments, cloud services, provider SDKs, queues, webhooks |
| Public contracts | API shape, response envelope, client-visible behavior |
| Cross-platform | browser/mobile/desktop split, native shell behavior, deep links |
| Existing behavior | thay đổi hành vi đã implement hoặc đã có test |
| Weak proof | thiếu hoặc chưa rõ checks quanh vùng bị ảnh hưởng |
| Multi-domain | thay đổi nhiều hơn một product domain |

## Classification

```text
0-1 flags:
  tiny hoặc normal, tùy code impact

2-3 flags:
  normal với validation mạnh hơn

4+ flags:
  high-risk

Bất kỳ hard gate nào:
  high-risk trừ khi human thu hẹp scope rõ ràng
```

Hard gates:

- Auth.
- Authorization.
- Data loss hoặc migration.
- Audit/security.
- External provider behavior.
- Gỡ bỏ hoặc làm yếu validation requirements.

## Intake Output

Cuối intake, agent phải có thể nói:

```text
Lane: normal
Reason: chạm API contract và screen behavior.
Docs: docs/product/features/orders/po.md, docs/product/features/orders/screens.md.
Story: docs/stories/US-001-order-list.md.
Validation: unit + manual screen check.
```
