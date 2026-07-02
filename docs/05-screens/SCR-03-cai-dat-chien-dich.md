# SCR-03 — Cài Đặt Chiến Dịch (キャンペーン設定)

## Overview

Màn hình tạo mới và chỉnh sửa chiến dịch. Giao diện multi-tab cho phép thiết lập từng phần độc lập. Chỉ cần nhập tab "Thiết lập cơ bản" để tạo chiến dịch; các tab khác có thể thiết lập sau.

## Display Conditions

Truy cập từ SCR-02: click "Đăng ký mới" (form trống) hoặc click chiến dịch đã có (load dữ liệu).

## Initial Display Behavior

**Tạo mới:** Tab "Thiết lập cơ bản" active, tất cả fields trống.
**Chỉnh sửa:** Load dữ liệu đã lưu, hiển thị trạng thái chiến dịch hiện tại.
Sau khi lưu Thiết lập cơ bản → tạo campaign record, trạng thái = "設定中 (Đang thiết lập)".
Khi đủ 3 mục (cơ bản + định dạng + ≥1 ô rút thăm) → tự động chuyển "未抽選 (Chưa rút thăm)".

## Screen Layout

Dựa trên mockup: `#2_キャンペーン設定_作成前.png`, `#2_キャンペーン設定_作成後.png`, `#2_キャンペーン設定_応募データフォーマット.png`, và các ảnh tab con.

### Header / Breadcrumb
- Breadcrumb: Danh sách chiến dịch > Cài đặt chiến dịch
- Tên chiến dịch (hiển thị sau khi tạo)
- Badge trạng thái chiến dịch

### Tab Navigation (ngang)

| Tab # | Tên Tab (VI) | Tên Tab (JP) | Ghi chú |
|-------|-------------|-------------|---------|
| 1 | Thiết lập cơ bản | 基本設定 | Bắt buộc tạo trước |
| 2 | Định dạng dữ liệu đăng ký | 応募データフォーマット | Bắt buộc |
| 3 | Cài đặt khung bốc thăm | 抽選枠設定 | Bắt buộc ≥1 |
| 4 | Kiểm tra trùng lặp | 重複チェック | Tùy chọn |
| 5 | Điều kiện tư cách | 適格条件 | Tùy chọn |
| 6 | Hệ số nhân | 倍率設定 | Tùy chọn |
| 7 | Cài đặt Double Chance | ダブルチャンス設定 | Ngoài phạm vi MVP |

---

### Tab 1 — Thiết Lập Cơ Bản (基本設定)

**Section: Thiết lập cơ bản**

| Field | Loại | Bắt buộc | Ghi chú |
|-------|------|----------|---------|
| CPID | Text input | ※ | Định danh MobileGet / TalkdeGet |
| Mã dự án | Text input | ※ | Định danh hệ thống cốt lõi |
| Tên khách hàng | Text input | ※ | |
| Tên chiến dịch | Text input | ※ | |
| Thời gian tổ chức — Từ | DateTime picker | ※ | |
| Thời gian tổ chức — Đến | DateTime picker | ※ | |
| Ngày rút thăm | Date picker | Không | |
| Cờ tự động xác nhận | Toggle / Checkbox | Không | ON = 当選/落選; OFF = 仮当選/落選 |

**Nút:**
- 「保存」(Lưu) — tạo/cập nhật chiến dịch
- 「キャンセル」(Hủy) — quay lại SCR-02

---

### Tab 2 — Định Dạng Dữ Liệu Đăng Ký (応募データフォーマット)

Cấu hình mapping cột CSV → trường hệ thống.

| Field | Loại | Bắt buộc | Ghi chú |
|-------|------|----------|---------|
| Họ tên — cột CSV | Text (ví dụ: "A", "C", "AZ") | ※ | Số thứ tự cột trong CSV |
| Furigana — cột CSV | Text | Không | |
| Địa chỉ — cột CSV | Text | Không | |
| Số điện thoại — cột CSV | Text | Không | |
| Email — cột CSV | Text | Không | |
| Hình ảnh hóa đơn — cột CSV | Text | Không | Có thể để trống (chiến dịch không yêu cầu hóa đơn) |
| Mục điều kiện tìm kiếm riêng | Danh sách cấu hình | Không | Chỉ định số thứ tự cột + tên hiển thị + loại so sánh |

> [MISSING — Mức độ: Trung bình] Cần danh sách đầy đủ các trường cá nhân có thể mapping. Tài liệu chỉ liệt kê ví dụ (họ tên, furigana, địa chỉ). Cần xác nhận với khách hàng tổng số trường và tên chính xác.

---

### Tab 3 — Cài Đặt Khung Bốc Thăm (抽選枠設定)

Dựa trên mockup: `#2_キャンペーン設定_抽選枠設定_基本設定.png`, `_口数設定.png`, `_等数設定.png`, `_倍率設定.png`, `_適格条件.png`, `_抽選枠判定条件.png`

**Danh sách ô rút thăm đã tạo** (panel trái hoặc danh sách trên)
- Nút 「追加」(Thêm ô rút thăm mới)
- Nút 「削除」(Xóa ô rút thăm)

**Form thiết lập từng ô rút thăm:**

*Sub-tab: Thiết lập cơ bản (基本設定)*

| Field | Loại | Bắt buộc | Ghi chú |
|-------|------|----------|---------|
| Tên ô rút thăm | Text input | ※ | |
| Số lượng trúng | Number input | ※ | |
| Có hạng giải không | Toggle | Không | ON → mở sub-section hạng giải |

*Sub-tab: Thiết lập số lượng (口数設定) — khi không có hạng giải*

| Field | Loại | Bắt buộc | Ghi chú |
|-------|------|----------|---------|
| Số lượng trúng | Number | ※ | |
| Điều kiện | Condition builder | Không | Thêm/xóa điều kiện |

*Sub-tab: Thiết lập hạng giải (等数設定) — khi có hạng giải*

| Field | Loại | Bắt buộc | Ghi chú |
|-------|------|----------|---------|
| Số hạng giải | Number | ※ | |
| Tên hạng giải N | Text | ※ | Cho từng hạng |
| Số lượng trúng hạng N | Number | ※ | Tổng = tổng số lượng trúng |

*Sub-tab: Điều kiện tư cách (適格条件)*
- Condition builder: thêm/xóa điều kiện hợp lệ cho ô rút thăm này

*Sub-tab: Điều kiện đánh giá khung (抽選枠判定条件)*
- Condition builder: logic xác định đăng ký thuộc ô rút thăm nào

*Sub-tab: Thiết lập tỷ lệ nhân (倍率設定)*

| Field | Loại | Bắt buộc | Ghi chú |
|-------|------|----------|---------|
| Tỷ lệ nhân | Number | ※ | Số lần nhân |
| Điều kiện áp dụng | Condition builder | ※ | |

---

### Tab 4 — Kiểm Tra Trùng Lặp (重複チェック)

Dựa trên mockup: `#2_キャンペーン設定_重複チェック*.png`

**Phần 1: Trùng lặp hóa đơn**

| Field | Loại | Ghi chú |
|-------|------|---------|
| Kiểm tra hóa đơn dùng nhiều lần | Toggle/Checkbox | |
| Kiểm tra nhiều hóa đơn giống nhau trong 1 đăng ký | Toggle/Checkbox | |
| Kiểm tra trong cùng chiến dịch | Toggle/Checkbox | Xuyên chiến dịch: ngoài phạm vi |

**Phần 2: Trùng lặp người trúng (同一応募者チェック)**

| Field | Loại | Ghi chú |
|-------|------|---------|
| Không cho phép cùng người trúng nhiều lần | Toggle | |
| Các tham số kiểm tra | Fields phụ | Hiển thị khi bật |

> Kiểm tra trùng lặp người đăng ký (applicant duplicate): ngoài phạm vi MVP.
> Kiểm tra xuyên chiến dịch: ngoài phạm vi MVP.

---

### Tab 5 — Điều Kiện Tư Cách (適格条件)

Dựa trên mockup: `#2_キャンペーン設定_適格条件*.png`, `#2_キャンペーン設定_条件グループ追加後.png`

**Condition Group Builder:**
- Thêm / xóa nhóm điều kiện (condition group)
- Trong mỗi nhóm: thêm / xóa điều kiện cụ thể
- Chọn loại điều kiện từ dropdown (ví dụ: tên sản phẩm, giá trị mua, ngày mua, v.v.)
- Chỉ định toán tử: =, ≠, >, <, contains, v.v.
- Nhập giá trị so sánh
- Logic giữa các nhóm: AND / OR

> [MISSING — Mức độ: Cao] Danh sách đầy đủ các loại điều kiện có thể chọn, tên và kiểu dữ liệu của từng loại, chưa được định nghĩa trong input. Cần xác nhận với khách hàng.

---

### Tab 6 — Hệ Số Nhân (倍率設定)

*(Xem Tab 3 Sub-tab Thiết lập tỷ lệ nhân — cấu hình tương tự nhưng ở cấp chiến dịch)*

---

### Tab 7 — Double Chance *(Ngoài phạm vi MVP)*

---

## Screen Actions

| Action | Trigger | Xử lý | Điều hướng sau |
|--------|---------|--------|----------------|
| Lưu thiết lập cơ bản | Click 保存 (Tab 1) | Tạo/cập nhật campaign | Reload SCR-03 với data đã lưu |
| Chuyển tab | Click tab | Load nội dung tab | Ở lại SCR-03 |
| Thêm ô rút thăm | Click 追加 (Tab 3) | Tạo ô rút thăm mới | Hiển thị form ô rút thăm mới |
| Xóa ô rút thăm | Click 削除 | Xác nhận → xóa | Reload danh sách ô |
| Xác nhận chiến dịch | Button 確定 (F-11) | Kiểm tra điều kiện → thay đổi trạng thái | Cập nhật badge trạng thái |
| Quay lại | Click Cancel / Breadcrumb | — | → SCR-02 |

## Screen Transition

- **Vào:** Từ SCR-02 (tạo mới hoặc chỉnh sửa)
- **Ra:** → SCR-02 (cancel/save), → SCR-04 (click xem danh sách ô rút thăm)
