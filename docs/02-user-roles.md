# 02 — Định Nghĩa Vai Trò Người Dùng

## Tổng Quan

Hệ thống xác thực qua SSO (GMO Trust Login). Thông tin người dùng được đồng bộ tự động khi đăng nhập thành công lần đầu — không cần đăng ký thủ công trong hệ thống.

Module **Quản lý người dùng** (CRUD) và **Quản lý quyền hạn** nằm **ngoài phạm vi MVP**.

## Vai Trò Đã Xác Định

Từ Functional Requirement (#48 — Quản lý quyền hạn), có đề cập hai vai trò điển hình:

### Role A — System Administrator (Quản trị viên hệ thống)
**Quyền đặc biệt (ví dụ từ tài liệu):**
- Quản lý người dùng
- Rút thăm lại (re-lottery)
- Nhập lại (re-import)
- Toàn bộ chức năng của Campaign Administrator

### Role B — Campaign Administrator (Quản trị viên chiến dịch)
**Quyền điển hình (ví dụ từ tài liệu):**
- Đăng ký / chỉnh sửa / xóa chiến dịch
- Đăng ký / chỉnh sửa / xóa điều kiện hợp lệ
- Tải xuống kết quả rút thăm

## Lưu Ý

> [MISSING — Mức độ: Cao] Danh sách đầy đủ các role và bảng phân quyền chi tiết (ai được làm gì) chưa được định nghĩa trong tài liệu input. Tài liệu gốc chỉ ghi "★Các biến thể của role?" — cần xác nhận với khách hàng trước khi thiết kế màn hình phân quyền.

> [MISSING — Mức độ: Trung bình] Chưa rõ role nào được thực hiện kiểm tra hợp lệ thủ công, thay đổi trạng thái ô rút thăm, xóa dữ liệu batch.

## Nguồn Tham Khảo
- Functional Requirement #42–45 (Quản lý người dùng — ngoài phạm vi)
- Functional Requirement #48 (Quản lý quyền hạn — ngoài phạm vi)
- Functional Requirement #47 (Đăng nhập SSO)
- Functional Requirement #49 (Quản lý log — dùng thông tin định danh từ GMO Trust)
