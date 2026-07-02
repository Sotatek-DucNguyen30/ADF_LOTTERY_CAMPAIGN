# 01 — Tổng Quan Dự Án

## 1. Thông Tin Cơ Bản

| Mục | Nội dung |
|-----|----------|
| Tên hệ thống | Hệ thống Quản lý Chiến dịch Rút thăm (Lottery Campaign Management System) |
| Viết tắt | ADF Lottery Campaign |
| Khách hàng | Alpha (tên khách hàng thực tế được nhập khi đăng ký từng chiến dịch) |
| Nhà phát triển | Sotatek / Guildworks |
| Mục tiêu triển khai | September 2026 (SSO GMO Trust Login dự kiến vận hành từ tháng 9/2026) |
| Ngày tài liệu | 2026-07-02 |

## 2. Mô Tả Hệ Thống

Hệ thống quản lý toàn bộ vòng đời của chiến dịch rút thăm trúng thưởng: từ thiết lập chiến dịch, nhập dữ liệu đăng ký (từ MobileGet / TalkdeGet), kiểm tra điều kiện hợp lệ (OCR hóa đơn + LLM), rút thăm, xác nhận kết quả, đến tải xuống kết quả.

Hệ thống là **công cụ nội bộ** dành cho nhân viên vận hành chiến dịch, không phải portal cho người tiêu dùng.

## 3. Phạm Vi MVP (v1 — bản 20260629)

### Trong phạm vi
- Đăng ký / chỉnh sửa / danh sách chiến dịch
- Thiết lập ô rút thăm (Lottery Slot)
- Thiết lập kiểm tra trùng lặp hóa đơn (trong phạm vi chiến dịch, loại bỏ xuyên chiến dịch)
- Thiết lập tỷ lệ nhân (multiplier)
- Thiết lập điều kiện hợp lệ (eligibility conditions)
- Nhập dữ liệu đăng ký từ CSV (MobileGet / TalkdeGet) — hình ảnh hóa đơn do khách hàng tải lên S3 ngoài hệ thống
- Nhập thử nghiệm (tối đa 100 dòng)
- OCR hóa đơn (Azure Document Intelligence + Gemini 3 Flash)
- Kiểm tra hợp lệ điều kiện đơn giản và phức tạp (LLM)
- Rút thăm (có tính tái lập)
- Xử lý xác nhận trúng / thua (auto & thủ công)
- Danh sách đăng ký / chi tiết đăng ký / chỉnh sửa đăng ký
- Tải xuống / tải lên kết quả rút thăm
- Đăng nhập SSO (GMO Trust Login)
- Giới hạn IP
- Xóa dữ liệu (batch)
- Quản lý log hệ thống
- Kiểm tra trùng lặp người trúng (trong chiến dịch)

### Ngoài phạm vi (Loại khỏi phạm vi)
- Kiểm tra trùng lặp xuyên chiến dịch
- Kiểm tra trùng lặp người đăng ký (applicant duplicate check)
- Tải xuống dữ liệu kết quả thực tế (actual results CSV)
- Cơ hội kép (Double Chance) — toàn bộ module
- Kiểm tra gian lận hóa đơn (fraud detection)
- Quản lý người dùng (User CRUD)
- Quản lý quyền hạn (Role management)
- Thay đổi / reset mật khẩu
- Khóa tài khoản (brute force protection)

## 4. Tech Stack

| Lớp | Công nghệ | Ghi chú |
|-----|-----------|---------|
| Backend | Python 3.14 + FastAPI (latest stable) | Auto-gen Swagger/OpenAPI |
| Frontend | TypeScript 5.9 + React 19 + Next.js 16.x | |
| Batch | Python 3.14 + Celery 5.x + Redis | Async image processing |
| RDBMS | MySQL 8.4 (Aurora MySQL ưu tiên) hoặc MS SQL Server 2025 | Quyết định qua thảo luận với Alpha |
| OCR | Azure Document Intelligence + Gemini 3 Flash | Gemini 3 Pro Image cho fraud (ngoài phạm vi) |
| AI/LLM | Gemini 3 Flash (PoC đã đạt accuracy) | ChatGPT 4o mini không sử dụng |
| Auth | GMO Trust Login (SSO) + AWS Cognito / ALB | Dự kiến tháng 9/2026 |
| Infrastructure | AWS (multi-AZ trong Tokyo region) | Xem infra diagram |

## 5. Kiến Trúc Tổng Quan

Theo infra diagram (`inputs/external-input/[Lottery Campaign] Infra_diagram.png`):
- Kiến trúc AWS, multi-AZ, Tokyo region
- ALB → Application servers (scale-out)
- Database scale-up
- S3 lưu trữ hình ảnh hóa đơn (khách hàng upload trực tiếp, ngoài luồng hệ thống)
- Redis cho Celery task queue

## 6. Người Dùng Mục Tiêu

Nhân viên vận hành chiến dịch nội bộ. Chi tiết role → xem `02-user-roles.md`.
