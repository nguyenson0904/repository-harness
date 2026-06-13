# Stories

Stories là các lát cắt implementation vừa đủ nhỏ.

Tạo story khi công việc lớn hơn một tiny edit:

```text
docs/stories/US-001-order-list.md
docs/stories/US-002-create-order.md
```

Dùng `docs/templates/story.md`.

## Status Values

| Status | Ý nghĩa |
| --- | --- |
| planned | Work đã được chấp nhận, chưa bắt đầu |
| in_progress | Đang build |
| implemented | Đã implement và có validation evidence |
| changed | Contract thay đổi sau implementation trước đó |
| retired | Không còn thuộc product contract |

## Story Closeout

Trước khi close story:

- Cập nhật status.
- Check acceptance criteria.
- Ghi validation đã chạy.
- Liệt kê files changed.
- Thêm follow-ups hoặc decisions khi cần.
