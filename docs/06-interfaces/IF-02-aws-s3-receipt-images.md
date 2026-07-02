# IF-02 — AWS S3 (Lưu Trữ Ảnh Hóa Đơn)

## Business Context

Ảnh hóa đơn (receipt images) do người đăng ký upload khi tham gia chiến dịch. Hệ thống cần truy xuất ảnh này để thực hiện OCR và kiểm tra hợp lệ.

## Destination System

AWS S3 (object storage)

## Overview

Ảnh hóa đơn **không** được upload qua hệ thống này. Khách hàng (Alpha) tự upload ảnh lên S3 bằng cơ chế bên ngoài hệ thống. Hệ thống chỉ đọc (read-only access) từ S3 dựa trên path/key được ghi trong CSV đăng ký.

## Input / Output

**Input:** Đường dẫn / key S3 từ dữ liệu CSV đăng ký (cột ảnh hóa đơn)
**Output:** Binary image data (JPG/PNG) để đưa vào OCR pipeline (Azure Document Intelligence + Gemini)

## Processing Timing

Được gọi trong batch pipeline: sau khi import CSV → khi xử lý OCR cho từng đăng ký.

## Connection Method

AWS SDK (S3 GetObject) — internal network access trong môi trường AWS.

## Data Format

Binary image (JPG / PNG). Một đăng ký có thể có nhiều ảnh hóa đơn.

> [MISSING — Mức độ: Cao] Chưa rõ: (1) Cấu trúc bucket/prefix S3. (2) Cách định danh ảnh từ CSV (URL đầy đủ hay chỉ key?). (3) IAM permission model. (4) Có cross-account access không? Cần xác nhận trước khi thiết kế batch pipeline.
