# IF-06 — Email Service (Thông Báo Hoàn Tất Xử Lý Async)

## Business Context

Khi các tác vụ xử lý batch async (kiểm tra hợp lệ thủ công, kiểm tra trùng lặp thủ công) hoàn tất, hệ thống cần thông báo cho operator qua email.

## Destination System

Email service (nhà cung cấp chưa được chỉ định — suy luận từ FR #24, #25)

## Overview

Sau khi batch job hoàn tất, Celery worker gửi email thông báo đến người dùng đã trigger tác vụ. Ngay sau khi trigger, UI hiển thị thông báo "Sẽ thông báo qua email khi hoàn tất".

## Input / Output

**Input:** Kết quả batch job (OK/NG counts, error details) + địa chỉ email người trigger
**Output:** Email thông báo hoàn tất

## Processing Timing

Async — sau khi Celery task group hoàn thành.

## Connection Method

> [MISSING — Mức độ: Trung bình] Nhà cung cấp email service chưa được chỉ định (AWS SES, SendGrid, v.v.). Cần xác nhận. Địa chỉ email người nhận lấy từ claims GMO Trust hay DB riêng?

## Data Format

Email HTML/plain text. Nội dung: loại tác vụ, số records xử lý, số OK, số NG, timestamp.

> [MISSING — Mức độ: Thấp] Template email (nội dung, format, ngôn ngữ) chưa được định nghĩa.
