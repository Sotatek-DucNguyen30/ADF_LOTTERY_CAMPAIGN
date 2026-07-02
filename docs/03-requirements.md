# 03 — Yêu Cầu Chức Năng & Phi Chức Năng

## A. Luồng Nghiệp Vụ Chính

```
[Cài đặt chiến dịch] → [Nhập dữ liệu đăng ký từ CSV] → [Rút thăm (batch)]
    → [OCR hóa đơn] → [Kiểm tra hợp lệ] → [Kiểm tra trùng lặp]
    → [Xác nhận trúng/thua] → [Tải xuống kết quả] → [Xóa dữ liệu]
```

### Trạng Thái Chiến Dịch

```
設定中 (Đang thiết lập)
  → [Khi có đủ: Thiết lập cơ bản + Định dạng dữ liệu + ≥1 ô rút thăm]
未抽選 (Chưa rút thăm)
  → [Xác nhận]
確定 (Đã xác nhận)
  → [Huỷ xác nhận]
  → [Kết thúc]
完了 (Hoàn thành)
  → [Có thể xóa khi đến tháng dự kiến hủy]
キャンセル (Huỷ)
```

### Trạng Thái Ô Rút Thăm

```
設定中 (Đang thiết lập) → 未抽選 (Chưa rút thăm) → 抽選済 (Đã rút thăm)
  → [Khi tất cả đăng ký liên kết ở trạng thái 当選/落選/NG]
確定 (Đã xác nhận)
```

### Trạng Thái Đăng Ký

```
未抽選 (Chưa rút thăm)
仮当選 (Tạm thời trúng) — khi cờ tự động xác nhận = OFF
当選 (Trúng) — khi cờ tự động xác nhận = ON, tất cả check OK
落選 (Thua)
NG — khi có ít nhất 1 check fail
```

## B. Yêu Cầu Chức Năng (MVP — Trong Phạm Vi)

### B1. Quản Lý Chiến Dịch

| # | Chức năng | Mô tả tóm tắt |
|---|-----------|---------------|
| F-01 | Đăng ký chiến dịch | Tạo mới chiến dịch. Bắt buộc nhập Thiết lập cơ bản trước. Thiết lập cơ bản xong → trạng thái "Đang thiết lập". Đủ 3 điều kiện → chuyển "Chưa rút thăm" |
| F-02 | Đăng ký ô rút thăm | Thiết lập 1..N ô rút thăm. Cấu hình: tên, số lượng trúng, có/không hạng giải |
| F-03 | Chỉnh sửa ô rút thăm | Xem và chỉnh sửa nội dung ô rút thăm đã đăng ký |
| F-04 | Kiểm soát chỉnh sửa ô rút thăm | Khi chiến dịch gốc = "Đã xác nhận" → không thể chỉnh sửa ô rút thăm. Khi ≥1 ô rút thăm "Đã xác nhận" → không thể nhập dữ liệu đăng ký |
| F-05 | Xóa ô rút thăm | Xóa ô rút thăm đã thiết lập |
| F-06 | Danh sách ô rút thăm | Xem danh sách ô rút thăm của chiến dịch. Header: Số quản lý rút thăm, Tên chiến dịch, Thời gian tổ chức |
| F-07 | Thiết lập kiểm tra trùng lặp hóa đơn | 0..N kiểm tra trùng lặp. 3 loại: (1) hóa đơn dùng nhiều lần, (2) nhiều hóa đơn giống nhau trong 1 đăng ký, (3) kiểm tra trong cùng chiến dịch. Kiểm tra xuyên chiến dịch: NGOÀI phạm vi |
| F-08 | Thiết lập kiểm tra trùng lặp người trúng | Trong chiến dịch. Xuyên chiến dịch: NGOÀI phạm vi |
| F-09 | Thiết lập tỷ lệ nhân | 1 đơn → N đơn khi đáp ứng điều kiện. Cấu hình: tỷ lệ nhân, điều kiện xác định đăng ký để áp dụng |
| F-10 | Chỉnh sửa chiến dịch | Xem và chỉnh sửa chiến dịch. Không thể sửa: Số quản lý rút thăm |
| F-11 | Thay đổi trạng thái chiến dịch | Xác nhận (tất cả ô rút thăm phải "Đã xác nhận") hoặc Hủy xác nhận. Khi xác nhận phải nhập tháng dự kiến hủy |
| F-12 | Danh sách chiến dịch | Xem danh sách. Cột: Số quản lý, Tên chiến dịch, Tên khách hàng, Trạng thái, Thời gian. Tìm kiếm: nhiều điều kiện |
| F-13 | Đăng ký điều kiện hợp lệ | 1..N điều kiện cho chiến dịch hoặc ô rút thăm. Đánh giá "đơn lẻ" hoặc "nhiều (xuyên suốt)" |
| F-14 | Xóa điều kiện hợp lệ | Xóa điều kiện đã thiết lập |

### B2. Quản Lý Rút Thăm & Đăng Ký

| # | Chức năng | Mô tả tóm tắt |
|---|-----------|---------------|
| F-15 | Danh sách đăng ký | 100 records/trang (có thể thay đổi, duy trì trong session). Cột: ID đăng ký, v.v. |
| F-16 | Kiểm tra trùng lặp thủ công | Thực hiện async. Thông báo qua email khi hoàn tất |
| F-17 | Thay đổi dữ liệu danh sách đăng ký | Thay đổi tự do trạng thái đăng ký. Không thể đưa trạng thái khác "Chưa rút thăm" về "Chưa rút thăm" |
| F-18 | Kiểm tra hợp lệ thủ công | Chọn từ danh sách, thực hiện async, thông báo email |
| F-19 | Chi tiết đăng ký | Xem toàn bộ nội dung đăng ký. Nếu giá trị cuối có phần mở rộng ảnh → hiển thị ảnh hóa đơn |
| F-20 | Chỉnh sửa đăng ký | Chỉ thay đổi được: Trạng thái đăng ký, Ghi chú |
| F-21 | Thay đổi trạng thái ô rút thăm | "抽選済" → "確定" khi tất cả đăng ký ở trạng thái 当選/落選/NG |
| F-22 | Tải xuống kết quả rút thăm | CSV + ảnh hóa đơn. Format: UTF-8/LF/CSV. Nội dung: thông tin người đăng ký, nội dung đăng ký, kết quả kiểm tra, kết quả rút thăm |
| F-23 | Tải lên kết quả rút thăm | Upload CSV chỉnh sửa từ file tải xuống. Có thể cập nhật: Trạng thái đăng ký, Hạng giải, Ghi chú |

### B3. Batch Processing

| # | Chức năng | Mô tả tóm tắt |
|---|-----------|---------------|
| F-24 | Nhập dữ liệu đăng ký | Upload CSV từ MobileGet/TalkdeGet. Hỗ trợ nhiều file, drag-and-drop. Ảnh hóa đơn khách hàng tự upload S3 ngoài hệ thống |
| F-25 | Nhập thử nghiệm | Như F-24 nhưng tối đa 100 dòng. Thực hiện kiểm tra hợp lệ cho tất cả dữ liệu (không phân biệt winner/loser) |
| F-26 | Xác định ứng viên rút thăm | Sắp xếp ngẫu nhiên có tính tái lập (reproducible random). Cùng seed → cùng thứ tự |
| F-27 | Kiểm tra trùng lặp | Thực hiện các kiểm tra đã cấu hình trong campaign |
| F-28 | Xử lý xác nhận trúng/thua | Auto-confirm (cờ ON): tất cả OK → 当選, có ≥1 NG → 落選 |
| F-29 | Xử lý xác nhận tạm thời | Auto-confirm (cờ OFF): tất cả OK → 仮当選, có ≥1 NG → 落選 |
| F-30 | OCR hóa đơn | Azure Document Intelligence + Gemini 3 Flash. Max = số lượng trúng × 2 |
| F-31 | Kiểm tra hợp lệ đơn giản | Điều kiện cấu hình sẵn, so sánh giá trị trực tiếp |
| F-32 | Kiểm tra hợp lệ phức tạp | LLM (Gemini) diễn giải điều kiện từ ngôn ngữ tự nhiên |

### B4. Xác Thực & Hệ Thống

| # | Chức năng | Mô tả tóm tắt |
|---|-----------|---------------|
| F-33 | Đăng nhập SSO | GMO Trust Login. Tự động đăng ký user vào DB hệ thống khi đăng nhập lần đầu |
| F-34 | Giới hạn IP | Hạn chế truy cập theo IP nguồn |
| F-35 | Xóa dữ liệu | Xóa batch chiến dịch có trạng thái 完了 và đã đến tháng dự kiến hủy |
| F-36 | Đo lường log hệ thống | Lưu toàn bộ log thao tác. Định danh user từ GMO Trust (không lưu user info trong DB riêng) |
| F-37 | Tham khảo log hệ thống | Xem danh sách log. Sắp xếp: giảm dần theo ngày giờ (mặc định). Tìm kiếm: ngày giờ thao tác, người dùng thao tác |

---

## C. Yêu Cầu Phi Chức Năng

### C1. Availability

| Mục | Yêu cầu |
|-----|---------|
| Uptime | 99.99% / năm |
| Thời gian chuyển đổi bảo trì | Cho phép vài giờ downtime cho bảo trì có kế hoạch |
| Mục tiêu phục hồi | Phục hồi trong 1 ngày làm việc (khi cần phục hồi dữ liệu) |
| Thảm họa quy mô lớn | Dùng nhiều data center cluster tách biệt vật lý trong Tokyo region. Khi 1 cluster lỗi: phục hồi trong 1 ngày. Thảm họa toàn Tokyo region: không tính |

### C2. Performance

| Đối tượng | Giá trị trung bình | Giá trị peak |
|-----------|-------------------|--------------|
| Số chiến dịch | 30 cases/tháng | 40 cases/ngày |
| Người đăng ký | 123,544 cases/tháng | 256,849 cases/ngày |
| Người trúng | 15,886 cases/tháng | 33,648 cases/ngày |
| Số hóa đơn | 247,087 sheets/tháng | 513,698 sheets/ngày |
| Xử lý người đăng ký | 7,400 cases/giờ | 30,000 cases/giờ |
| Xử lý người trúng | 630 cases/giờ | 10,000 cases/giờ |

**Mục tiêu tốc độ phản hồi màn hình:**

| Màn hình | Mục tiêu |
|----------|----------|
| Tổng thể | 1 giây (trung bình) |
| Danh sách chiến dịch (30 records) | 2 giây (trung bình) |
| Chi tiết chiến dịch | 1 giây (trung bình) |
| Danh sách ô rút thăm (100 records) | 2 giây (trung bình) |
| Danh sách đăng ký (100 records) | 2 giây (trung bình) |
| Danh sách đăng ký (1000 records) | 20 giây (trung bình) |
| Nhập DL + Rút thăm + Kiểm tra hợp lệ (TB) | 0.8 giây/record |
| Nhập DL + Rút thăm + Kiểm tra hợp lệ (Peak) | 6.5 giây/record |

### C3. Scalability

- Database: Scale-up (nâng cấu hình)
- Application: Scale-out (tăng server/container)

### C4. Operability & Maintainability

| Mục | Yêu cầu |
|-----|---------|
| Giờ vận hành | 24/7, trừ bảo trì có kế hoạch |
| Backup DB | Hàng đêm, lưu 7 ngày |
| Monitoring | Giám sát resource usage, phát hiện thiếu tài nguyên |
| Môi trường hỗ trợ | Windows 11 + Edge (chỉ PC layout, không hỗ trợ smartphone) |
| Bảo trì | Báo trước 1 tuần khi cần shutdown. Thực hiện ban đêm/sáng sớm |
| Manual | Bên chịu trách nhiệm tự tạo (Guildworks hỗ trợ) |

### C5. Migration

> [MISSING — Mức độ: Thấp] Phương pháp migration, lịch trình, dữ liệu/cơ sở vật chất cần định nghĩa riêng.

### C6. Security

- Vulnerability assessment (app + platform) theo quy định của Alpha trước khi go-live
- Giới hạn IP truy cập
- Đăng nhập SSO, không lưu password trong hệ thống
- Log toàn bộ thao tác có định danh user
