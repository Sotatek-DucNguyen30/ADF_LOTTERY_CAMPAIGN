# SCR-05 — Danh Sách Đăng Ký (応募一覧)

## Overview

Danh sách dữ liệu đăng ký của một ô rút thăm cụ thể. Cho phép thực hiện kiểm tra hợp lệ thủ công, kiểm tra trùng lặp, thay đổi trạng thái hàng loạt, và điều hướng sang chi tiết từng đăng ký.

## Display Conditions

Truy cập từ SCR-04, với context ô rút thăm đã chọn.

## Initial Display Behavior

- Hiển thị header: thông tin chiến dịch + ô rút thăm
- Danh sách đăng ký, 100 records/trang mặc định (số lượng có thể thay đổi, duy trì trong session)
- Trạng thái kiểm tra: chưa kiểm tra / đang kiểm tra / đã kiểm tra
- Panel lọc mặc định đóng

## Screen Layout

Dựa trên mockup: `#4_応募一覧.png`, `#4_応募一覧_適格チェック中.png`, `#4_応募一覧_適格チェック後.png`, `#4_応募一覧_適格チェック後絞り込みOPEN.png`, `#4_応募一覧_選択中.png`

### Header Thông Tin
- Tên chiến dịch / Số quản lý
- Tên ô rút thăm
- Trạng thái ô rút thăm (badge)

### Khu Vực Action (trên bảng)
- Nút **「適格チェック」(Kiểm tra hợp lệ thủ công)** — kích hoạt khi đã chọn ≥1 record
- Nút **「重複チェック」(Kiểm tra trùng lặp thủ công)**
- Nút **「ダウンロード」(Tải xuống kết quả rút thăm)**
- Nút **「アップロード」(Tải lên kết quả rút thăm)**
- Nút **「絞り込み」** — toggle panel lọc
- Dropdown **件数切替** (thay đổi số records/trang): 100 / 500 / 1000

### Panel Lọc (collapsible)
- ID đăng ký (text)
- Trạng thái đăng ký (dropdown/checkbox nhiều chọn)
- Kết quả kiểm tra hợp lệ (dropdown)
- Kết quả kiểm tra trùng lặp (dropdown)
- Mục điều kiện tìm kiếm riêng (các field được cấu hình trong tab Định dạng dữ liệu của chiến dịch)

### Trạng Thái Trong Khi Kiểm Tra
- Overlay / progress indicator khi 適格チェック đang chạy async
- Thông báo: "Sẽ thông báo qua email khi hoàn tất"

### Bảng Danh Sách Đăng Ký

| Cột | Nội dung |
|-----|----------|
| Checkbox chọn | Multi-select |
| ID đăng ký | |
| Họ tên | |
| Trạng thái đăng ký | Badge (未抽選 / 仮当選 / 当選 / 落選 / NG) |
| Kết quả kiểm tra hợp lệ | OK / NG / Chưa kiểm tra |
| Kết quả kiểm tra trùng lặp | OK / NG / Chưa kiểm tra |
| Hạng giải | Hiển thị khi ô rút thăm có hạng giải |
| Ngày giờ đăng ký | |
| Ghi chú | |
| Thao tác | Link sang SCR-06 |

> [MISSING — Mức độ: Trung bình] Cột hiển thị đầy đủ cần xác nhận. Các mục điều kiện tìm kiếm riêng sẽ hiện thị như thêm cột vào bảng hay chỉ dùng trong filter?

## Input-Output Item List

### Điều Kiện Lọc (Input)
| Field | Loại | Bắt buộc |
|-------|------|----------|
| ID đăng ký | Text | Không |
| Trạng thái đăng ký | Multi-select | Không |
| Kết quả kiểm tra hợp lệ | Dropdown | Không |
| Kết quả kiểm tra trùng lặp | Dropdown | Không |
| Mục tìm kiếm riêng (dynamic) | Text/Number | Không |

### Upload Kết Quả (Input)
| Field | Loại | Bắt buộc | Ghi chú |
|-------|------|----------|---------|
| File CSV kết quả rút thăm | File upload | ※ | Chỉnh sửa từ file tải xuống |

## Screen Actions

| Action | Trigger | Xử lý | Điều hướng sau |
|--------|---------|--------|----------------|
| Kiểm tra hợp lệ thủ công | Chọn records → click 適格チェック | Async. Thông báo email khi xong | Hiển thị progress, reload sau khi xong |
| Kiểm tra trùng lặp thủ công | Click 重複チェック | Async. Thông báo email khi xong | Reload |
| Tải xuống | Click ダウンロード | Sinh CSV + zip ảnh hóa đơn | Download file |
| Tải lên | Click アップロード → chọn file | Cập nhật hàng loạt trạng thái / hạng giải / ghi chú | Reload |
| Thay đổi số records/trang | Dropdown 件数切替 | Lưu vào session | Reload bảng |
| Xem chi tiết | Click row / nút thao tác | — | → SCR-06 |

## Screen Transition

- **Vào:** Từ SCR-04
- **Ra:** → SCR-06 (chi tiết đăng ký)
