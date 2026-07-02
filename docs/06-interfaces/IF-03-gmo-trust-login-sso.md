# IF-03 — GMO Trust Login (SSO Authentication)

## Business Context

Hệ thống sử dụng SSO qua GMO Trust Login để xác thực người dùng, thay vì quản lý username/password riêng. Dự kiến vận hành từ tháng 9/2026.

## Destination System

GMO Trust Login (IDaaS) — AWS Cognito / ALB Authentication

## Overview

Khi người dùng đăng nhập, được redirect sang GMO Trust Login để xác thực. Sau khi xác thực thành công, hệ thống nhận thông tin người dùng qua callback. Nếu user chưa tồn tại trong DB hệ thống → tự động đăng ký. Thông tin định danh từ GMO Trust được dùng cho log hệ thống.

## Input / Output

**Output từ hệ thống → GMO Trust:** Redirect request (SAML/OIDC)
**Input từ GMO Trust → hệ thống:** User identity claims (email, tên, role/group, v.v.)

## Processing Timing

Real-time — mỗi lần người dùng đăng nhập.

## Connection Method

SAML 2.0 hoặc OIDC (qua AWS Cognito / ALB). Phương thức chính xác cần xác nhận theo cấu hình của Alpha.

## Data Format

JWT token hoặc SAML assertion chứa user identity claims.

> [MISSING — Mức độ: Cao] Cần xác nhận: (1) Giao thức chính xác (SAML hay OIDC). (2) Các claims được cung cấp (đặc biệt là role/group để phân quyền). (3) Thời điểm go-live tháng 9/2026 có ảnh hưởng đến timeline phát triển không — cần giải pháp tạm thời trước đó?
