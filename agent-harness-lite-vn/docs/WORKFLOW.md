# Workflow

Harness này cố ý chỉ dùng Markdown. Policy nằm trong docs. Tiến độ nằm trong
story files. Quyết định bền vững nằm trong decision records.

## Work Loop

```text
User prompt
  -> phân loại input type và lane
  -> tìm product docs liên quan
  -> tạo hoặc cập nhật story khi cần
  -> lập hướng implement nhỏ nhất và an toàn nhất
  -> implement
  -> validate
  -> cập nhật story status và evidence
  -> cập nhật product docs, decisions, hoặc backlog nếu cần
  -> final response
```

## Thứ Tự Nguồn Sự Thật

```text
User prompt hoặc spec được cung cấp
  input material cho công việc mới

docs/product/*
  product contract đang sống

docs/stories/*
  lát cắt implement, tiến độ, validation notes, follow-ups

docs/decisions/*
  quyết định kiến trúc, data, API, security, hoặc process cần tồn tại lâu dài
```

Trước khi implement, product docs mô tả intent. Sau khi implement, product docs
cộng với validation thực thi được trở thành living contract.

## Output Của Task

Mỗi task có thể tạo hai loại output:

- Product delta: source code, tests, config, API shape, data model, UI, hoặc
  product docs.
- Harness delta: story updates, decision records, validation notes, backlog
  items, hoặc chỉnh sửa template/process.

## Quy Tắc Story

Dùng story khi công việc lớn hơn một thay đổi tiny.

Tạo story từ `docs/templates/story.md` và đặt dưới `docs/stories/`.

Một story nên có:

- goal,
- product docs liên quan,
- acceptance criteria,
- implementation notes,
- validation checklist,
- status,
- files changed,
- follow-ups.

## Quy Tắc Decision

Tạo decision record từ `docs/templates/decision.md` khi task thay đổi:

- hướng kiến trúc,
- ownership hoặc strategy của database/schema,
- public API shape,
- auth hoặc authorization rules,
- audit/security behavior,
- validation requirements,
- source-of-truth hierarchy.

## Checklist Trước Khi Kết Thúc

Trước final response:

- Cập nhật status và validation notes trong story.
- Cập nhật product docs nếu contract thay đổi.
- Thêm decision record nếu có quyết định bền vững.
- Thêm backlog follow-up nếu còn việc quan trọng.
- Nêu validation đã chạy và validation chưa chạy.
