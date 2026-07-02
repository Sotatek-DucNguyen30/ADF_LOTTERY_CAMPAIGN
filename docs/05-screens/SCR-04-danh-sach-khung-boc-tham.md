# SCR-04 — Danh Sách Khung Bốc Thăm (抽選枠一覧)

## Overview

Danh sách các ô rút thăm (Lottery Slot) liên kết với một chiến dịch. Từ đây có thể nhập dữ liệu đăng ký và điều hướng sang danh sách đăng ký.

## Display Conditions

Truy cập từ SCR-02 hoặc SCR-03, với context chiến dịch đã chọn.

## Initial Display Behavior

- Hiển thị header thông tin chiến dịch (tên, trạng thái, thời gian)
- Danh sách tất cả ô rút thăm của chiến dịch
- Panel lọc mặc định đóng

## Screen Layout

Dựa trên mockup: `#3_抽選枠一覧.png`, `#3_抽選枠一覧_絞り込みOPEN.png`, `#3_抽選枠一覧_応募取り込み.png`, `#3_抽選枠一覧_応募取り込み中.png`, `#3_抽選枠一覧_応募取り込み後.png`

### Header Thông Tin Chiến Dịch
- Số quản lý rút thăm
- Tên chiến dịch
- Trạng thái chiến dịch (badge)
- Thời gian tổ chức

### Khu Vực Action
- Nút **「応募取り込み」(Nhập dữ liệu đăng ký)** — mở dialog upload CSV
- Nút **「テスト取り込み」(Nhập thử nghiệm)** — upload CSV tối đa 100 dòng
- Nút **「絞り込み」** — toggle panel lọc

### Dialog Nhập Dữ Liệu Đăng Ký
Hiển thị khi click 応募取り込み:
- Vùng drag-and-drop upload file CSV
- Hỗ trợ upload nhiều file cùng lúc
- Trạng thái trong khi nhập: progress indicator
- Trạng thái sau khi nhập: kết quả (thành công / lỗi)

### Panel Lọc (collapsible)
- Tên ô rút thăm (text, khớp một phần)
- Trạng thái ô rút thăm (dropdown)
- Ngày rút thăm (date range)

### Bảng Danh Sách Ô Rút Thăm

| Cột | Nội dung |
|-----|----------|
| Tên ô rút thăm | |
| Trạng thái | Badge (設定中 / 未抽選 / 抽選済 / 確定) |
| Số lượng trúng | |
| Số lượng đăng ký | |
| Số lượng đã rút thăm | |
| Ngày rút thăm | |
| Thao tác | Link sang SCR-05 (Danh sách đăng ký) |

> [MISSING — Mức độ: Trung bình] Danh sách cột đầy đủ cần xác nhận từ mockup chi tiết. Suy luận từ FR #6 (Danh sách ô rút thăm) và ảnh mockup.

## Input-Output Item List

### Nhập Dữ Liệu (Upload)
| Field | Loại | Bắt buộc | Ghi chú |
|-------|------|----------|---------|
| File CSV | File upload | ※ | Từ MobileGet / TalkdeGet. Nhiều file cùng lúc |

### Điều Kiện Lọc
| Field | Loại | Bắt buộc |
|-------|------|----------|
| Tên ô rút thăm | Text | Không |
| Trạng thái | Dropdown | Không |
| Ngày rút thăm | Date range | Không |

## Screen Actions

| Action | Trigger | Xử lý | Điều hướng sau |
|--------|---------|--------|----------------|
| Nhập dữ liệu đăng ký | Click 応募取り込み | Upload CSV → batch import async | Hiển thị trạng thái "đang nhập", sau đó "hoàn thành" |
| Nhập thử nghiệm | Click テスト取り込み | Như trên, tối đa 100 dòng, kiểm tra hợp lệ tất cả | Kết quả kiểm tra |
| Xem danh sách đăng ký | Click ô rút thăm / nút thao tác | — | → SCR-05 (context ô rút thăm đã chọn) |

## Screen Transition

- **Vào:** Từ SCR-02 hoặc SCR-03
- **Ra:** → SCR-05 (chọn ô rút thăm cụ thể)
