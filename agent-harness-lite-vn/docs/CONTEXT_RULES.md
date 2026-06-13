# Context Rules

Context rules giúp agent biết cần đọc gì và khi nào nên dừng đọc. Mục tiêu
không phải là đọc thật nhiều context; mục tiêu là đọc đúng context cho phase
hiện tại.

## Luôn Đọc Trước

Với mọi task:

- `AGENTS.md`
- `README.md`
- `docs/WORKFLOW.md`
- `docs/FEATURE_INTAKE.md`
- `docs/CONTEXT_RULES.md`

## Intake Phase

Đọc để phân loại request và tìm surface bị ảnh hưởng.

| Source | Tiny | Normal | High-risk |
| --- | --- | --- | --- |
| `docs/product/*` | Nếu liên quan trực tiếp | Must | Must |
| `docs/stories/*` | Nếu story đã tồn tại | Must nếu story tồn tại | Must |
| `docs/ARCHITECTURE.md` | Skip trừ khi structural | Should | Must |
| `docs/decisions/*` | Skip trừ khi liên quan | Should nếu chạm architecture/data/API | Must |

## Planning Phase

Đọc để chọn hướng implement nhỏ nhất, an toàn nhất và xác định proof cần có.

| Source | Tiny | Normal | High-risk |
| --- | --- | --- | --- |
| Files sẽ sửa | Must | Must | Must |
| File lân cận cùng pattern | Should | Must | Must |
| `docs/templates/story.md` | Skip | Must khi tạo/cập nhật story | Must |
| Product docs liên quan | Should nếu behavior đổi | Must | Must |
| Decisions liên quan | Skip trừ khi chạm tới | Should | Must |

## Implementation Phase

Giữ context implementation trong phạm vi:

- files đang sửa,
- adjacent patterns,
- product docs liên quan,
- story liên quan,
- architecture docs nếu thay đổi structure/boundary.

Không đọc lịch sử không liên quan sau khi lane, affected files, và validation
path đã rõ.

## Validation Phase

Trước khi claim hoàn thành, đọc:

- acceptance criteria trong story,
- validation checklist trong story,
- test/build commands khả dụng từ project docs,
- validation report template nếu proof đáng chú ý hoặc high-risk.

## Closeout Phase

Trước final response:

- Đọc lại story hoặc product docs đã thay đổi.
- Kiểm tra changed files.
- Cập nhật validation notes và follow-ups.
- Thêm decisions/backlog items nếu task thay đổi durable truth hoặc phát hiện
  friction.

## Retrieval Triggers

| Trigger | Action |
| --- | --- |
| Task chạm database schema hoặc data ownership | Đọc `docs/ARCHITECTURE.md`, product ERD, và decisions liên quan |
| Task đổi API shape hoặc client-visible behavior | Đọc product docs, screen docs, và stories liên quan |
| Task chạm auth, authorization, audit/security, data loss, hoặc provider behavior | Treat as high-risk |
| Task đổi source-of-truth hoặc validation policy | Đọc workflow, intake, architecture, và decisions trước khi sửa |
| Task làm lộ confusion lặp lại hoặc docs bị thiếu | Cập nhật docs trực tiếp hoặc thêm backlog item |
