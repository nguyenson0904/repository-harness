# Hướng Dẫn Cho Agent

Repo này dùng một agent harness gọn nhẹ, chỉ dựa trên Markdown.

Trước khi sửa code hoặc tài liệu sản phẩm, hãy đọc:

- `README.md`
- `docs/WORKFLOW.md`
- `docs/FEATURE_INTAKE.md`
- `docs/CONTEXT_RULES.md`
- `docs/CODING_RULES.md`

Khi công việc chạm tới kiến trúc, API, database, boundary, provider, hoặc hành
vi liên module, đọc thêm:

- `docs/ARCHITECTURE.md`
- Các file liên quan trong `docs/product/`
- Các file liên quan trong `docs/stories/`
- Các file liên quan trong `docs/decisions/`

## Quy Tắc Vận Hành

- Phân loại mọi request thành `tiny`, `normal`, hoặc `high-risk` trước khi sửa.
- Giữ product truth trong `docs/product/`.
- Giữ các lát cắt triển khai trong `docs/stories/`.
- Giữ quyết định bền vững trong `docs/decisions/`.
- Dùng checklist Markdown để theo dõi trạng thái và validation. Bản lite này
  không có CLI, database, matrix, codegen, hoặc hidden state.
- Sau khi implement, cập nhật story liên quan với status, validation đã chạy,
  file đã sửa, và follow-up.
- Nếu thiếu rule/template/product doc làm việc bị vướng, cập nhật docs trực
  tiếp hoặc thêm follow-up vào `docs/stories/backlog.md`.

## Định Nghĩa Done

Một task chỉ được xem là xong khi:

- Thay đổi được yêu cầu đã hoàn thành hoặc blocker đã được ghi rõ.
- Product docs và story liên quan đã được cập nhật.
- Validation khả dụng đã chạy, hoặc lý do không chạy đã được ghi lại.
- Quyết định kiến trúc/sản phẩm cần tồn tại lâu dài đã được ghi trong
  `docs/decisions/`.
- Final response nêu rõ đã thay đổi gì, đã validate gì, và chưa làm gì.
