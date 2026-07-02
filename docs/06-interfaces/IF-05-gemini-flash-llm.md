# IF-05 — Gemini 3 Flash (AI/LLM — Kiểm Tra Hợp Lệ & OCR Diễn Giải)

## Business Context

Dùng Gemini 3 Flash để: (1) diễn giải kết quả OCR thành dữ liệu có cấu trúc từ ảnh hóa đơn, (2) kiểm tra điều kiện hợp lệ phức tạp dựa trên ngôn ngữ tự nhiên. PoC đã xác nhận độ chính xác đủ dùng không cần ChatGPT 4o mini.

## Destination System

Google Gemini API (Gemini 3 Flash model)

## Overview

Được gọi trong batch pipeline (Celery). Nhận dữ liệu OCR từ Azure Document Intelligence + thông tin đăng ký, trả về dữ liệu có cấu trúc và kết quả đánh giá điều kiện. Gemini 3 Pro Image (ngoài phạm vi MVP) sẽ dùng cho fraud detection.

## Input / Output

**Luồng OCR → Structured Data:**
- Input: Raw OCR text từ Azure Document Intelligence + prompt diễn giải
- Output: JSON có cấu trúc (tên sản phẩm, giá, ngày mua, tên cửa hàng, v.v.)

**Luồng Kiểm Tra Hợp Lệ Phức Tạp:**
- Input: Dữ liệu có cấu trúc của hóa đơn + dữ liệu đăng ký + mô tả điều kiện bằng ngôn ngữ tự nhiên
- Output: OK / NG + lý do

## Processing Timing

Async batch — trong pipeline Celery workers, sau bước OCR.

## Connection Method

Google Gemini REST API / Python SDK (`google-genai`). Xác thực qua API Key hoặc Service Account.

## Data Format

- Input: JSON + text prompt
- Output: JSON (structured extraction) hoặc text (eligibility judgment)

> [MISSING — Mức độ: Trung bình] Prompt template cho từng use case (OCR diễn giải, kiểm tra hợp lệ) chưa được định nghĩa. Cần thiết kế prompt engineering riêng dựa trên PoC đã có.
