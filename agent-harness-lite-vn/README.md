# Agent Harness Lite VN

`agent-harness-lite-vn` là một project harness gọn nhẹ, chỉ dùng Markdown, dành
cho coding agent.

Nó giữ các phần hữu ích của repository harness:

- entrypoint ổn định cho agent,
- bước phân loại công việc đơn giản,
- product docs như hợp đồng sản phẩm sống,
- story nhỏ vừa đủ để implement,
- decision records,
- validation checklist,
- backlog/follow-up.

Nó cố ý loại bỏ:

- CLI tooling,
- SQLite hoặc database vận hành,
- test matrix commands,
- code generation,
- release workflows,
- scaffold theo ngôn ngữ/framework,
- application source code.

Mục tiêu là giúp repo dễ làm việc hơn với AI coding agent mà không làm quy
trình khó hiểu.

## Cấu Trúc Thư Mục

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

## Luồng Làm Việc Điển Hình

```text
ý định của user
  -> phân loại lane
  -> tìm product docs liên quan
  -> tạo hoặc cập nhật story
  -> implement
  -> chạy validation
  -> cập nhật checklist trong story
  -> ghi decision hoặc follow-up nếu cần
  -> final response
```

## Đặt Tài Liệu Feature Ở Đâu

Với feature mới, đặt source material tại:

```text
docs/product/features/<feature-name>/
  README.md
  po.md
  erd.md
  screens.md
  assets/
```

Sau đó tạo implementation stories tại:

```text
docs/stories/US-001-<short-name>.md
```

Story nên link ngược về product docs mà nó implement.
