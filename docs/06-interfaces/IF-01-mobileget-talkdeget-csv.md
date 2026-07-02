# IF-01 — MobileGet / TalkdeGet (Nguồn Dữ Liệu Đăng Ký CSV)

## Business Context

Dữ liệu đăng ký của người tiêu dùng tham gia chiến dịch được thu thập qua hai hệ thống bên ngoài: MobileGet và TalkdeGet. Operator tải CSV từ các hệ thống này rồi upload vào hệ thống quản lý chiến dịch.

## Destination System

MobileGet / TalkdeGet (hệ thống thu thập đăng ký của khách hàng Alpha)

## Overview

Hệ thống này không kết nối trực tiếp (không có API call). Operator tải xuống CSV từ MobileGet/TalkdeGet thủ công, sau đó upload vào hệ thống qua SCR-04.

## Input / Output

**Output từ MobileGet/TalkdeGet → Input vào hệ thống:**
- File CSV chứa thông tin đăng ký: họ tên, furigana, địa chỉ, SĐT, email, ngày giờ đăng ký, và các cột dữ liệu tùy theo chiến dịch
- Cột ảnh hóa đơn: giá trị cuối chứa đường dẫn/tên file ảnh (nếu chiến dịch yêu cầu hóa đơn)
- Encoding: không rõ (cần xác nhận)

> [MISSING — Mức độ: Cao] Format CSV chi tiết (số cột, tên cột, encoding, delimiter, có header row không) chưa được định nghĩa. Cần xác nhận với khách hàng để thiết kế mapping.

## Processing Timing

Thủ công (manual upload) — operator thực hiện khi cần nhập dữ liệu đăng ký.

## Connection Method

File upload (không có API). Operator download CSV từ MobileGet/TalkdeGet, sau đó upload qua giao diện SCR-04 (drag-and-drop hoặc file picker, hỗ trợ multi-file).

## Data Format

CSV — chi tiết format theo cấu hình của từng chiến dịch (mapping cột trong Tab 2 SCR-03).
