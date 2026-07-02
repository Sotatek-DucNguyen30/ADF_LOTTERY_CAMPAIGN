# 00 — Báo Cáo Missing (MISSING Report)

> Tạo ngày: 2026-07-02 | Phiên bản input: Functional Requirement bản 20260629

---

## 1. Bảng Tổng Hợp Theo Nhóm

### Nhóm: Project Overview

| Mục thiếu | File liên quan | Mức độ | Câu hỏi cho khách hàng |
|-----------|----------------|--------|------------------------|
| Tên chính thức / thương hiệu của hệ thống | 01-project-overview.md | Thấp | Tên hệ thống chính thức để dùng trong tài liệu và UI là gì? |
| Timeline phát triển chi tiết | 01-project-overview.md | Trung bình | Kế hoạch sprint/phase cụ thể từ tháng 7/2026 đến go-live là gì? |

---

### Nhóm: User Roles

| Mục thiếu | File liên quan | Mức độ | Câu hỏi cho khách hàng |
|-----------|----------------|--------|------------------------|
| Danh sách đầy đủ tên các role và số lượng role | 02-user-roles.md | **Cao** | Hệ thống có bao nhiêu role? Tên chính xác của từng role là gì? |
| Bảng phân quyền chi tiết (role × chức năng) | 02-user-roles.md | **Cao** | Mỗi role được làm những gì và không được làm gì? (Đặc biệt: ai được rút thăm lại, nhập lại, kiểm tra hợp lệ thủ công, xóa dữ liệu batch?) |
| Role nào nhận email thông báo async | 02-user-roles.md | Trung bình | Email thông báo khi kiểm tra hợp lệ/trùng lặp xong gửi cho ai? Người trigger hay tất cả operator? |

---

### Nhóm: Requirements

| Mục thiếu | File liên quan | Mức độ | Câu hỏi cho khách hàng |
|-----------|----------------|--------|------------------------|
| Migration method, schedule, data scope | 03-requirements.md | Thấp | Có dữ liệu cần migrate từ hệ thống cũ không? Nếu có, từ hệ thống nào? |
| Giải pháp xác thực tạm thời trước tháng 9/2026 (GMO Trust go-live) | 03-requirements.md | **Cao** | Trước khi GMO Trust Login vận hành (tháng 9/2026), hệ thống dùng cơ chế xác thực nào cho môi trường dev/staging/UAT? |

---

### Nhóm: Screen List

| Mục thiếu | File liên quan | Mức độ | Câu hỏi cho khách hàng |
|-----------|----------------|--------|------------------------|
| Screen Transition chi tiết: Trigger, Precondition, Parameter Passing, Error Destination | 04-screen-list.md | Trung bình | Không có tài liệu screen transition diagram chi tiết. Có thể cung cấp luồng điều hướng đầy đủ không? |

---

### Nhóm: SCR-01 (Đăng nhập)

| Mục thiếu | File liên quan | Mức độ | Câu hỏi cho khách hàng |
|-----------|----------------|--------|------------------------|
| Mockup màn hình đăng nhập | SCR-01-dang-nhap.md | Thấp | Màn hình đăng nhập có thiết kế riêng hay chỉ hiển thị nút SSO? |
| Nội dung thông báo lỗi khi SSO thất bại | SCR-01-dang-nhap.md | Thấp | Khi xác thực GMO Trust thất bại, hiển thị thông báo gì? |

---

### Nhóm: SCR-02 (Danh sách chiến dịch)

| Mục thiếu | File liên quan | Mức độ | Câu hỏi cho khách hàng |
|-----------|----------------|--------|------------------------|
| Số records mặc định/trang | SCR-02-danh-sach-chien-dich.md | Thấp | Danh sách chiến dịch hiển thị bao nhiêu records/trang mặc định? |
| Sắp xếp mặc định | SCR-02-danh-sach-chien-dich.md | Thấp | Thứ tự sắp xếp mặc định của danh sách chiến dịch là gì? |

---

### Nhóm: SCR-03 (Cài đặt chiến dịch)

| Mục thiếu | File liên quan | Mức độ | Câu hỏi cho khách hàng |
|-----------|----------------|--------|------------------------|
| Danh sách đầy đủ các trường cá nhân trong Tab Định dạng dữ liệu đăng ký | SCR-03-cai-dat-chien-dich.md | **Cao** | Tab "Định dạng dữ liệu đăng ký" cần cấu hình mapping cho những trường nào? (Họ tên, furigana, địa chỉ... còn trường nào khác?) |
| Danh sách loại điều kiện có thể chọn trong Condition Builder (Tab điều kiện tư cách, điều kiện đánh giá khung) | SCR-03-cai-dat-chien-dich.md | **Cao** | Khi cấu hình điều kiện hợp lệ, operator có thể chọn những loại điều kiện nào? (tên sản phẩm, giá, ngày, thương hiệu, v.v.) Kiểu dữ liệu và toán tử nào được hỗ trợ? |
| Validation rules cho từng field | SCR-03-cai-dat-chien-dich.md | Trung bình | Mỗi field có validation gì? (max length, format, giá trị min/max cho số lượng trúng, v.v.) |
| Error messages khi validation fail | SCR-03-cai-dat-chien-dich.md | Trung bình | Nội dung thông báo lỗi khi nhập sai là gì? |
| Mục nào không thể chỉnh sửa sau khi chiến dịch tạo | SCR-03-cai-dat-chien-dich.md | Trung bình | FR ghi "Số quản lý rút thăm không thể chỉnh sửa" và đánh dấu "※Còn mục nào khác?" — cần xác nhận danh sách đầy đủ |

---

### Nhóm: SCR-04 (Danh sách khung bốc thăm)

| Mục thiếu | File liên quan | Mức độ | Câu hỏi cho khách hàng |
|-----------|----------------|--------|------------------------|
| Danh sách cột đầy đủ trong bảng ô rút thăm | SCR-04-danh-sach-khung-boc-tham.md | Trung bình | Bảng danh sách ô rút thăm hiển thị những cột nào? (FR #6 liệt kê header nhưng không liệt kê toàn bộ cột bảng) |
| Luồng xử lý lỗi khi import CSV | SCR-04-danh-sach-khung-boc-tham.md | Trung bình | Khi file CSV có lỗi format hoặc dữ liệu không hợp lệ, hệ thống xử lý như thế nào? Báo lỗi toàn bộ hay import phần hợp lệ? |

---

### Nhóm: SCR-05 (Danh sách đăng ký)

| Mục thiếu | File liên quan | Mức độ | Câu hỏi cho khách hàng |
|-----------|----------------|--------|------------------------|
| Danh sách cột đầy đủ trong bảng | SCR-05-danh-sach-dang-ky.md | Trung bình | Bảng danh sách đăng ký hiển thị những cột nào mặc định? Có thể ẩn/hiện cột không? |
| Mục điều kiện tìm kiếm riêng hiển thị như thêm cột hay chỉ trong filter | SCR-05-danh-sach-dang-ky.md | Thấp | Khi chiến dịch có mục tìm kiếm riêng, nó hiển thị như cột trong bảng hay chỉ như filter panel? |

---

### Nhóm: SCR-06 (Chi tiết đăng ký)

| Mục thiếu | File liên quan | Mức độ | Câu hỏi cho khách hàng |
|-----------|----------------|--------|------------------------|
| Có hiển thị kết quả OCR chi tiết không | SCR-06-chi-tiet-dang-ky.md | Trung bình | Màn hình chi tiết đăng ký có hiển thị dữ liệu OCR đã trích xuất (tên sản phẩm, giá...) không? |
| Nội dung lý do NG từ kiểm tra hợp lệ | SCR-06-chi-tiet-dang-ky.md | Trung bình | Khi kết quả kiểm tra = NG, có hiển thị lý do chi tiết từ LLM không? Format như thế nào? |

---

### Nhóm: SCR-SYS (Quản lý log)

| Mục thiếu | File liên quan | Mức độ | Câu hỏi cho khách hàng |
|-----------|----------------|--------|------------------------|
| Cấu trúc log entry chi tiết (các loại log, các field) | SCR-SYS-quan-ly-log.md | Trung bình | Log hệ thống ghi nhận những loại thao tác nào? Mỗi log entry có những field gì? Có thể export log ra CSV không? |

---

### Nhóm: Interfaces

| Mục thiếu | File liên quan | Mức độ | Câu hỏi cho khách hàng |
|-----------|----------------|--------|------------------------|
| Format CSV chi tiết từ MobileGet/TalkdeGet (số cột, tên cột, encoding, delimiter) | IF-01-mobileget-talkdeget-csv.md | **Cao** | File CSV tải từ MobileGet/TalkdeGet có format như thế nào? Encoding? Có header row? Tên và thứ tự các cột cố định hay thay đổi theo chiến dịch? |
| Cấu trúc S3 bucket, cách định danh ảnh từ CSV, IAM permissions | IF-02-aws-s3-receipt-images.md | **Cao** | Ảnh hóa đơn lưu ở S3 bucket nào? CSV chứa URL đầy đủ hay chỉ key? Account AWS có phải cùng account không? |
| Giao thức SSO chính xác (SAML/OIDC), claims được cung cấp, giải pháp trước tháng 9/2026 | IF-03-gmo-trust-login-sso.md | **Cao** | GMO Trust Login dùng SAML hay OIDC? Claims trả về có bao gồm role/group để phân quyền không? |
| Danh sách các mục OCR cụ thể cần trích xuất (tên file spec OCR items riêng) | IF-04-azure-document-intelligence-ocr.md | **Cao** | Tài liệu tham khảo về "các mục OCR cụ thể" được đề cập trong FR nhưng không được cung cấp. File spec đó ở đâu? |
| Nhà cung cấp email service, địa chỉ email người nhận lấy từ đâu | IF-06-email-notification.md | Trung bình | Email thông báo dùng dịch vụ gì (AWS SES, SendGrid...)? Địa chỉ email người nhận lấy từ GMO Trust claims hay từ DB riêng? |

---

## 2. Nguồn Input Còn Trống Hoàn Toàn

| Thư mục / File | Nội dung cần bổ sung |
|----------------|---------------------|
| `inputs/overview/` | **Thư mục trống** — Cần: tài liệu tổng quan dự án (Project Brief / PRD) của Alpha |
| `inputs/requirement/screen-detail/detail/` | **Thư mục trống** — Cần: tài liệu mô tả chi tiết từng màn hình (screen spec sheet) |
| Spec OCR items | FR #30 đề cập "xem tài liệu tham khảo" nhưng file này không được cung cấp trong inputs |
| Infra diagram | File `inputs/external-input/[Lottery Campaign] Infra_diagram.png` có trong thư mục nhưng không thể phân tích nội dung chi tiết |

---

## 3. Top Việc Cần Làm Trước Khi Vào Bước DESIGN

Danh sách ưu tiên theo nguyên tắc: càng ảnh hưởng nhiều màn hình / nhiều component → ưu tiên càng cao.

### Ưu Tiên CAO (Block toàn bộ thiết kế nếu thiếu)

1. **Format CSV MobileGet/TalkdeGet** (IF-01)
   — Ảnh hưởng: Tab Định dạng dữ liệu (SCR-03), Import logic (SCR-04), Danh sách đăng ký (SCR-05), Chi tiết đăng ký (SCR-06), toàn bộ batch pipeline
   — Câu hỏi: Cấu trúc CSV đầy đủ?

2. **Danh sách và bảng phân quyền Role** (02-user-roles)
   — Ảnh hưởng: Thiết kế authentication/authorization toàn hệ thống, ẩn/hiện các button theo role
   — Câu hỏi: Có bao nhiêu role? Bảng phân quyền?

3. **Giải pháp xác thực trước tháng 9/2026** (IF-03, 03-requirements)
   — Ảnh hưởng: Toàn bộ luồng đăng nhập và phân quyền khi phát triển
   — Câu hỏi: Dùng gì cho dev/UAT trước khi GMO Trust live?

4. **Spec OCR items** (IF-04)
   — Ảnh hưởng: Schema DB cho kết quả OCR, prompt engineering Gemini, condition builder điều kiện hợp lệ
   — Câu hỏi: File tài liệu tham khảo OCR ở đâu?

5. **Danh sách loại điều kiện trong Condition Builder** (SCR-03 Tab 5)
   — Ảnh hưởng: Thiết kế UI condition builder, schema lưu trữ điều kiện, logic batch kiểm tra hợp lệ
   — Câu hỏi: Có những loại điều kiện nào?

6. **Cấu trúc S3 và cách định danh ảnh** (IF-02)
   — Ảnh hưởng: Thiết kế batch OCR pipeline
   — Câu hỏi: Bucket structure, URL hay key trong CSV?

### Ưu Tiên TRUNG BÌNH (Có thể bắt đầu thiết kế nhưng cần xác nhận trước khi code)

7. Danh sách fields mapping trong Tab Định dạng dữ liệu đăng ký (SCR-03)
8. Validation rules và error messages toàn bộ form (SCR-03)
9. Danh sách cột đầy đủ SCR-04, SCR-05
10. Nhà cung cấp email service và nguồn email address (IF-06)
11. Cấu trúc log entry chi tiết (SCR-SYS)

### Ưu Tiên THẤP (Có thể để sau, không block thiết kế)

12. Mockup màn hình đăng nhập (SCR-01)
13. Số records/trang và sort mặc định SCR-02
14. Migration method và schedule
15. Template email thông báo
