# SCR-SYS — Quản Lý Log Hệ Thống (ログ管理)

## Overview

Màn hình xem danh sách log thao tác của toàn hệ thống. Định danh người dùng lấy từ thông tin xác thực GMO Trust (không lưu user info riêng trong DB).

## Display Conditions

Người dùng đã đăng nhập. Quyền xem log tùy theo role.

## Initial Display Behavior

- Hiển thị danh sách log, sắp xếp giảm dần theo ngày giờ thao tác (mặc định)
- Người dùng có thể đổi sang tăng dần

## Screen Layout

Không có mockup riêng trong input.

### Khu Vực Tìm Kiếm / Lọc
- Ngày giờ thao tác — Từ ~ Đến (datetime range picker)
- Người dùng thao tác (text, tìm theo định danh GMO Trust)
- Loại log (dropdown) — nếu có phân loại

### Bảng Danh Sách Log

| Cột | Nội dung |
|-----|----------|
| Ngày giờ thao tác | Timestamp |
| Người dùng thao tác | Định danh từ GMO Trust |
| Loại thao tác | Tên chức năng / hành động |
| Đối tượng thao tác | Campaign ID, Application ID, v.v. |
| Chi tiết | Nội dung thao tác (tóm tắt) |

> [MISSING — Mức độ: Trung bình] Cấu trúc chi tiết của log entry (các loại log cụ thể, trường hiển thị, có thể export không) chưa được định nghĩa. Cần xác nhận với khách hàng.

## Input-Output Item List

### Điều Kiện Tìm Kiếm
| Field | Loại | Bắt buộc |
|-------|------|----------|
| Ngày giờ thao tác (Từ) | Datetime | Không |
| Ngày giờ thao tác (Đến) | Datetime | Không |
| Người dùng thao tác | Text | Không |
| Loại log | Dropdown | Không |

## Screen Actions

| Action | Trigger | Xử lý | Điều hướng sau |
|--------|---------|--------|----------------|
| Tìm kiếm | Click 検索 | Filter danh sách | Reload bảng |
| Đổi thứ tự sắp xếp | Click header cột ngày giờ | Toggle ASC/DESC | Reload bảng |

## Screen Transition

- **Vào:** Từ sidebar navigation
- **Ra:** Không có điều hướng ra màn hình khác
