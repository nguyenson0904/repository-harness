# Coding Rules

Dùng file này cho các quy ước code riêng của project mà agent phải tuân thủ
trong mọi thay đổi code.

Đây là nội dung mẫu. Hãy chỉnh lại theo project thật.

## Naming

- Tên entity, class, type, interface, enum, database table, column, API field,
  event phải viết bằng tiếng Anh.
- Không đặt tên domain concept hoặc entity bằng tiếng Việt trong source code.
- Tên biến local cũng nên dùng tiếng Anh, trừ khi giá trị đó là localization key
  hoặc fixture phục vụ test.
- Dùng cùng một domain name xuyên suốt product docs, code, database và API.

Nên dùng:

```text
Customer
OrderItem
PaymentStatus
created_at
```

Tránh:

```text
KhachHang
DonHang
TrangThaiThanhToan
ngay_tao
```

## Code Comments

- Comment code nên viết bằng tiếng Việt có dấu.
- Chỉ thêm comment khi cần giải thích business intent, tradeoff không hiển
  nhiên, hoặc edge case mà code không tự nói rõ.
- Không thêm comment chỉ để diễn giải lại dòng code bên dưới.
- Public API docs dùng ngôn ngữ mà project hoặc consumer yêu cầu. Nếu không có
  yêu cầu riêng, ưu tiên tiếng Anh cho public API docs và tiếng Việt cho
  internal implementation comments.

Nên dùng:

```text
// Giữ trạng thái cũ để tránh mất dữ liệu khi provider trả về timeout.
```

Tránh:

```text
// Set status to pending.
```

## Localization

- Không hardcode text tiếng Việt trong source code production.
- Mọi text hiển thị cho user phải đi qua localization function, translation
  file, hoặc message catalog của project.
- Khi thêm UI string mới, thêm localization key và translation entry tương ứng.
- Không ghép câu localized từ nhiều mảnh nếu ngữ pháp có thể thay đổi theo ngôn
  ngữ. Ưu tiên full sentence key với interpolation placeholders.
- Exception chỉ áp dụng cho tests, mocks, debug-only logs, hoặc seed data khi
  text đó không thể xuất hiện trong production UI.

Pattern nên dùng:

```text
t("orders.create.success")
```

Tránh:

```text
"Tạo đơn hàng thành công"
```

## Errors And Logs

- User-visible errors phải được localization.
- Developer logs có thể dùng tiếng Anh hoặc tiếng Việt, nhưng phải nhất quán
  trong project.
- Logs không được chứa secrets, tokens, passwords, hoặc personal data trừ khi
  product đã có safe audit policy rõ ràng.

## Tests

- Tên test nên mô tả behavior bằng tiếng Anh, trừ khi test suite hiện tại có
  convention khác.
- Test fixtures có thể chứa tiếng Việt khi test localization, rendering,
  search, encoding, hoặc ví dụ sản phẩm.
- Nếu test thêm user-visible text, assert theo localization keys hoặc rendered
  localized output theo pattern của project.

## Review Checklist

Trước khi close task, kiểm tra:

- [ ] Entity/domain names mới dùng tiếng Anh.
- [ ] Database/API fields dùng tiếng Anh và nhất quán với product docs.
- [ ] Code comments tuân thủ rule ngôn ngữ comment của project.
- [ ] Không hardcode text tiếng Việt trong production code.
- [ ] User-facing text mới đi qua localization.
- [ ] Exception đã được ghi trong story hoặc implementation notes.
