# IF-04 — Azure Document Intelligence (OCR Hóa Đơn)

## Business Context

Trích xuất text và layout từ ảnh hóa đơn. Kết quả OCR được dùng làm input cho Gemini để chuyển đổi thành dữ liệu có cấu trúc phục vụ kiểm tra hợp lệ.

## Destination System

Azure Document Intelligence (Microsoft Azure)

## Overview

Nhận ảnh hóa đơn (binary/URL), trả về text + layout có cấu trúc. Được gọi trong batch pipeline của Celery workers. Kết quả được kết hợp với Gemini 3 Flash để diễn giải nghiệp vụ.

## Input / Output

**Input:** Ảnh hóa đơn (JPEG/PNG) — binary hoặc URL
**Output:** Structured text + bounding boxes (tên sản phẩm, giá, ngày, cửa hàng, v.v.)

## Processing Timing

Async batch — được trigger sau khi import CSV và xác định thứ tự ứng viên rút thăm. Max records = số lượng trúng × 2.

## Connection Method

Azure REST API / Azure SDK (Python). Xác thực qua Azure Managed Identity hoặc API Key.

## Data Format

JSON response từ Azure Document Intelligence API (Document Analysis result).

> [MISSING — Mức độ: Trung bình] Danh sách các mục OCR cụ thể cần trích xuất (tên sản phẩm, giá, ngày, v.v.) được đề cập trong FR nhưng chỉ có trong "tài liệu tham khảo" chưa được cung cấp. Cần file spec OCR items riêng.
