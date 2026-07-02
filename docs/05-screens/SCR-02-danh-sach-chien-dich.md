# SCR-02 — Danh Sách Chiến Dịch (キャンペーン一覧)

## Overview

Màn hình danh sách toàn bộ chiến dịch đã đăng ký. Là trang đầu tiên sau khi đăng nhập thành công.

## Display Conditions

Người dùng đã đăng nhập.

## Initial Display Behavior

- Hiển thị danh sách chiến dịch, sắp xếp mặc định theo ngày tạo giảm dần
- Panel lọc/tìm kiếm mặc định đóng (collapsed)
- Phân trang mặc định (suy luận từ pattern 100 records/trang của danh sách đăng ký)

## Screen Layout

Dựa trên mockup: `#1_キャンペーン一覧.png`, `#1_キャンペーン一覧_絞り込みOPEN.png`

### Sidebar (trái)
- Navigation menu dọc
- Các mục điều hướng chính: Danh sách chiến dịch, Quản lý log (suy luận từ sơ đồ trang)

### Header (trên cùng)
- Tên hệ thống
- Thông tin user đang đăng nhập (góc phải)
- Nút Đăng xuất (góc phải)

### Main Area
**Khu vực action (trên bảng):**
- Nút **「新規登録」(Đăng ký mới)** — tạo chiến dịch mới → điều hướng sang SCR-03
- Nút/Link **「絞り込み」(Lọc/Tìm kiếm)** — toggle mở/đóng panel lọc

**Panel lọc (collapsible)** — hiển thị khi mở:
- Trường: Số quản lý rút thăm (text input)
- Trường: Tên chiến dịch (text input, khớp một phần)
- Trường: Tên khách hàng (text input, khớp một phần)
- Trường: Trạng thái chiến dịch (dropdown/checkbox)
- Trường: Thời gian tổ chức — Từ ~ Đến (date range picker)
- Nút **「検索」(Tìm kiếm)**
- Nút **「クリア」(Xóa điều kiện)**

**Bảng danh sách:**

| Cột | Nội dung |
|-----|----------|
| Số quản lý rút thăm | ID duy nhất của chiến dịch |
| Tên chiến dịch | Tên campaign |
| Tên khách hàng | Tên client |
| Trạng thái | Badge màu (設定中 / 未抽選 / 確定 / 完了 / キャンセル) |
| Thời gian tổ chức | Từ ~ Đến |
| Thao tác | Link/Button điều hướng sang SCR-03 |

**Phân trang (dưới bảng):**
- Hiển thị số trang, nút prev/next

> [MISSING — Mức độ: Thấp] Chưa rõ: số records mặc định/trang cho danh sách chiến dịch. Target response time = 2 giây với 30 records (từ NFR).

## Input-Output Item List

### Điều kiện tìm kiếm (Input)

| Tên field | Loại | Bắt buộc | Ghi chú |
|-----------|------|----------|---------|
| Số quản lý rút thăm | Text | Không | Khớp chính xác hoặc một phần |
| Tên chiến dịch | Text | Không | Khớp một phần |
| Tên khách hàng | Text | Không | Khớp một phần |
| Trạng thái chiến dịch | Multi-select / dropdown | Không | |
| Thời gian tổ chức — Từ | Date | Không | |
| Thời gian tổ chức — Đến | Date | Không | |

### Kết quả hiển thị (Output)

| Tên cột | Nguồn dữ liệu | Ghi chú |
|---------|---------------|---------|
| Số quản lý rút thăm | Campaign.lottery_mgmt_no | |
| Tên chiến dịch | Campaign.name | |
| Tên khách hàng | Campaign.client_name | |
| Trạng thái | Campaign.status | Badge màu |
| Thời gian tổ chức | Campaign.period_from ~ period_to | |

## Screen Actions

| Action | Trigger | Xử lý | Điều hướng sau |
|--------|---------|--------|----------------|
| Đăng ký mới | Click nút 新規登録 | — | → SCR-03 (form trống) |
| Tìm kiếm | Click 検索 | Filter danh sách theo điều kiện | Reload bảng |
| Xóa điều kiện | Click クリア | Reset tất cả filter | Reload bảng với tất cả records |
| Xem / Chỉnh sửa chiến dịch | Click row hoặc nút thao tác | — | → SCR-03 (chiến dịch đã chọn) |
| Mở/đóng panel lọc | Click 絞り込み | Toggle panel | Ở lại SCR-02 |

## Screen Transition

- **Vào:** Sau login thành công (SCR-01), hoặc từ SCR-03 nhấn Back
- **Ra:** → SCR-03 (tạo mới hoặc chỉnh sửa)
