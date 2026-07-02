# SCR-06 — Chi Tiết Đăng Ký (応募詳細)

## Overview

Hiển thị toàn bộ thông tin của một bản ghi đăng ký. Cho phép xem ảnh hóa đơn, chỉnh sửa trạng thái và ghi chú.

## Display Conditions

Truy cập từ SCR-05, với context bản ghi đăng ký đã chọn.

## Initial Display Behavior

- Load toàn bộ thông tin đăng ký
- Nếu dữ liệu đăng ký có trường giá trị cuối mang phần mở rộng ảnh (jpg, png, v.v.) → hiển thị thumbnail ảnh hóa đơn
- Nếu có nhiều ảnh hóa đơn → hiển thị nhiều thumbnail theo hàng ngang

## Screen Layout

Dựa trên mockup: `#5_応募詳細.png`, `#5_応募詳細_画像にレシートが複数枚の場合.png`, `#5_応募詳細_画像拡大モーダル.png`, `画像拡大モーダル.png`

### Header / Breadcrumb
- Danh sách chiến dịch > Tên chiến dịch > Danh sách khung bốc thăm > Tên ô rút thăm > Danh sách đăng ký > Chi tiết đăng ký
- ID đăng ký

### Section 1 — Thông Tin Đăng Ký

| Field | Nội dung |
|-------|----------|
| ID đăng ký | Hiển thị |
| Trạng thái đăng ký | Dropdown (editable): 未抽選 / 仮当選 / 当選 / 落選 / NG |
| Hạng giải | Dropdown (editable, chỉ khi ô rút thăm có hạng giải) |
| Ghi chú | Textarea (editable) |

### Section 2 — Nội Dung Khi Đăng Ký (Tất Cả Dữ Liệu CSV)

- Hiển thị tất cả cột từ CSV đăng ký theo mapping đã cấu hình
- Họ tên, furigana, địa chỉ, số điện thoại, email, ngày giờ đăng ký, v.v.
- Các trường mở rộng theo cấu hình từng chiến dịch

### Section 3 — Hình Ảnh Hóa Đơn

- Hiển thị thumbnail từng ảnh hóa đơn
- Khi có nhiều hóa đơn: hiển thị theo hàng (horizontal scroll hoặc grid)
- Click thumbnail → mở Modal phóng to

### Modal Phóng To Ảnh Hóa Đơn
- Hiển thị ảnh kích thước lớn
- Nút đóng modal (X)
- Nút điều hướng prev/next khi có nhiều ảnh

### Section 4 — Kết Quả Kiểm Tra

| Field | Nội dung |
|-------|----------|
| Kết quả kiểm tra hợp lệ | OK / NG / Chưa kiểm tra + chi tiết lý do |
| Kết quả kiểm tra trùng lặp | OK / NG / Chưa kiểm tra + chi tiết |

> [MISSING — Mức độ: Trung bình] Cần xác nhận: kết quả kiểm tra hiển thị chi tiết như thế nào (chỉ OK/NG hay kèm thông điệp lý do từ LLM)? Có hiển thị kết quả OCR không?

## Input-Output Item List

### Editable Fields
| Field | Loại | Điều kiện chỉnh sửa |
|-------|------|---------------------|
| Trạng thái đăng ký | Dropdown | Không thể đưa về 未抽選 nếu đang ở trạng thái khác |
| Hạng giải | Dropdown | Chỉ khi ô rút thăm có hạng giải |
| Ghi chú | Textarea | Luôn editable |

### Read-only Fields
| Field | Nguồn |
|-------|-------|
| ID đăng ký | DB |
| Tất cả dữ liệu CSV | CSV import |
| Kết quả kiểm tra | Batch process |
| Ảnh hóa đơn | S3 |

## Screen Actions

| Action | Trigger | Xử lý | Điều hướng sau |
|--------|---------|--------|----------------|
| Lưu chỉnh sửa | Click 保存 | Cập nhật trạng thái / hạng giải / ghi chú | Reload SCR-06 |
| Phóng to ảnh | Click thumbnail | Mở modal | Ở lại SCR-06 |
| Đóng modal | Click X / click ngoài | Đóng modal | Ở lại SCR-06 |
| Quay lại | Click Back / Breadcrumb | — | → SCR-05 |

## Screen Transition

- **Vào:** Từ SCR-05
- **Ra:** → SCR-05 (quay lại)
