# SCR-01 — Đăng Nhập

## Overview

Màn hình đăng nhập SSO. Người dùng được redirect sang GMO Trust Login để xác thực, sau đó redirect về hệ thống.

## Display Conditions

Khi người dùng chưa đăng nhập hoặc session hết hạn.

## Initial Display Behavior

- Hiển thị nút "Đăng nhập bằng GMO Trust Login"
- Nếu truy cập URL cần xác thực khi chưa đăng nhập → redirect về màn hình này

## Screen Layout

Dựa trên sơ đồ trang (so_do_trang_tieng_viet.pdf) — không có mockup riêng cho màn hình đăng nhập.

**Cấu trúc suy luận từ luồng SSO:**
- Logo / tên hệ thống (center)
- Nút "Đăng nhập" → redirect sang GMO Trust Login
- (Tùy chọn) Thông báo lỗi xác thực nếu redirect về với lỗi

> [MISSING — Mức độ: Thấp] Không có mockup cho màn hình login. Cần xác nhận: có hiển thị thông báo lỗi khi SSO thất bại không, và nội dung thông báo là gì.

## Input-Output Item List

| Item | Loại | Bắt buộc | Ghi chú |
|------|------|----------|---------|
| Nút Đăng nhập | Button | — | Trigger redirect sang GMO Trust Login |

## Screen Actions

| Action | Trigger | Xử lý | Điều hướng sau |
|--------|---------|--------|----------------|
| Đăng nhập | Click nút đăng nhập | Redirect sang GMO Trust Login (SSO) | Sau xác thực thành công → SCR-02 Danh sách chiến dịch |
| Xác thực thất bại | Callback từ SSO với lỗi | Hiển thị thông báo lỗi | Ở lại SCR-01 |

## Screen Transition

- **Vào:** Trực tiếp (chưa login) hoặc redirect từ bất kỳ màn hình nào
- **Ra (thành công):** → SCR-02 Danh sách chiến dịch
- **Liên quan:** Đặt lại MK (Yêu cầu) → Đặt lại MK (Thực hiện) → SCR-01 *(ngoài phạm vi MVP)*
