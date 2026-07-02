# 04 — Danh Sách Màn Hình & Sơ Đồ Điều Hướng

## Sơ Đồ Điều Hướng

Nguồn: `inputs/screen-detail/screen-list/so_do_trang_tieng_viet.pdf`

### Nhóm XÁC THỰC
- Đặt lại MK (Yêu cầu) → Đặt lại MK (Thực hiện) → **[SCR-01] Đăng nhập** ← Trang đầu tiên sau đăng nhập

### Nhóm CHIẾN DỊCH
- **[SCR-02] Danh sách chiến dịch** ↔ **[SCR-03] Cài đặt chiến dịch**
  - Từ SCR-03 mở ra các tab con:
    - Cài đặt cơ bản
    - Định dạng DL đăng ký
    - Cài đặt khung bốc thăm
    - Kiểm tra trùng lặp
    - Điều kiện tư cách
    - Hệ số nhân
    - Cài đặt Double Chance *(ngoài phạm vi MVP)*

### Nhóm BỐC THĂM & ĐĂNG KÝ
- **[SCR-04] Danh sách khung bốc thăm** → **[SCR-05] Danh sách đăng ký** → **[SCR-06] Chi tiết đăng ký**

### Nhóm DOUBLE CHANCE *(ngoài phạm vi MVP)*
- [SCR-DC1] Danh sách Double Chance → [SCR-DC2] DS đăng ký Double Chance → [SCR-DC3] Chi tiết ĐK Double Chance

### Nhóm NGƯỜI DÙNG & HỆ THỐNG *(User CRUD ngoài phạm vi MVP)*
- [SCR-USR1] Danh sách người dùng → Đăng ký người dùng → Chỉnh sửa người dùng
- **[SCR-SYS] Quản lý Log** *(trong phạm vi MVP)*

---

## Danh Sách Màn Hình — Trong Phạm Vi MVP

| Screen ID | Tên Màn Hình (VI) | Tên Màn Hình (JP) | Nhóm | File Chi Tiết |
|-----------|-------------------|--------------------|------|---------------|
| SCR-01 | Đăng nhập | ログイン | Xác thực | [SCR-01-dang-nhap.md](05-screens/SCR-01-dang-nhap.md) |
| SCR-02 | Danh sách chiến dịch | キャンペーン一覧 | Chiến dịch | [SCR-02-danh-sach-chien-dich.md](05-screens/SCR-02-danh-sach-chien-dich.md) |
| SCR-03 | Cài đặt chiến dịch | キャンペーン設定 | Chiến dịch | [SCR-03-cai-dat-chien-dich.md](05-screens/SCR-03-cai-dat-chien-dich.md) |
| SCR-04 | Danh sách khung bốc thăm | 抽選枠一覧 | Bốc thăm | [SCR-04-danh-sach-khung-boc-tham.md](05-screens/SCR-04-danh-sach-khung-boc-tham.md) |
| SCR-05 | Danh sách đăng ký | 応募一覧 | Bốc thăm | [SCR-05-danh-sach-dang-ky.md](05-screens/SCR-05-danh-sach-dang-ky.md) |
| SCR-06 | Chi tiết đăng ký | 応募詳細 | Bốc thăm | [SCR-06-chi-tiet-dang-ky.md](05-screens/SCR-06-chi-tiet-dang-ky.md) |
| SCR-SYS | Quản lý log hệ thống | ログ管理 | Hệ thống | [SCR-SYS-quan-ly-log.md](05-screens/SCR-SYS-quan-ly-log.md) |

## Danh Sách Màn Hình — Ngoài Phạm Vi MVP (Tham Khảo)

| Screen ID | Tên Màn Hình (VI) | Ghi Chú |
|-----------|-------------------|---------|
| SCR-DC1 | Danh sách Double Chance | Toàn module DC ngoài phạm vi |
| SCR-DC2 | DS đăng ký Double Chance | |
| SCR-DC3 | Chi tiết ĐK Double Chance | |
| SCR-USR1 | Danh sách người dùng | User CRUD ngoài phạm vi |
| SCR-USR2 | Đăng ký người dùng | |
| SCR-USR3 | Chỉnh sửa người dùng | |
