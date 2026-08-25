# HT HOME — Nền tảng web cho thuê phòng trọ & hệ thống quản lý môi giới

Đồ án môn học — Trường Đại học Công nghệ Thông tin, ĐHQG-HCM.

Nền tảng web cho thuê phòng trọ / căn hộ dịch vụ / ký túc xá, kết nối **khách thuê – nhân viên môi giới (sale) – admin** trên cùng một hệ thống. Chạy thật trên Cloudflare (chi phí gần bằng 0), dữ liệu lưu bền trên cơ sở dữ liệu đám mây, ảnh lưu trên object storage.

## 🔗 Truy cập

- **Trang khách (công khai):** https://hthome.thanghost.io.vn
- **Khu nội bộ (đăng nhập):** https://hthome.thanghost.io.vn/dangnhap-noibo.html
  - Tài khoản demo: **0900000001** · mật khẩu **123456** (quyền Admin)

## 🧩 Chức năng chính

**Website khách:** trang chủ + tìm/lọc phòng theo khu vực/giá/loại, tìm nâng cao theo tiện ích, chi tiết phòng (gallery ảnh/video/bản đồ), so sánh phòng, tài khoản khách, chat tư vấn, đặt lịch xem.

**Khu nội bộ (sale & admin):** dashboard, kho phòng, CRM khách hàng (kanban), deal & hợp đồng, doanh thu & hoa hồng, quản lý tòa nhà & phòng, lịch hẹn, quỹ nội bộ, bảng tin, quản lý nhân viên & phân quyền — đầy đủ **Thêm / Sửa / Xoá**, dữ liệu lưu bền.

## 🛠 Công nghệ

- **Frontend:** HTML/CSS/JS thuần, mobile-first, PWA (cài như app), component dùng chung.
- **Backend:** Cloudflare Pages Functions (`functions/api/*`) — REST API.
- **Dữ liệu:** Cloudflare D1 (SQLite) — bảng khách/giao dịch/lịch hẹn/toà nhà/nhân viên/bảng tin.
- **Ảnh:** Cloudflare R2 (object storage) qua `/api/upload` → phục vụ ở `/img/<key>`.
- **Triển khai:** Cloudflare Pages + CI/CD (GitHub Actions), tên miền riêng.

## 📁 Cấu trúc

```
*.html              các trang (khách + nội bộ)
assets/css          tokens, base, components, internal (design system Navy + Gold)
assets/js           ht-ui.js (component chung + PWA), ht-internal.js (sidebar + guard)
data.js             danh mục toà nhà/phòng (view khách) + helper
functions/api/      API D1: khach, giao-dich, lich-hen, toa-nha, nhan-vien, bang-tin, upload
functions/img/      phục vụ ảnh từ R2
db/                 schema + seed dữ liệu mẫu
manifest.json, sw.js  cấu hình PWA
```

## 🗄 Cơ sở dữ liệu (Cloudflare D1)

Tạo bảng từ `db/schema.sql` + `db/schema-noibo.sql`, nạp dữ liệu mẫu từ `db/seed.sql` + `db/seed-noibo.sql`. Binding `DB` (D1) và `IMAGES` (R2) cấu hình trong Cloudflare Pages project.

---

Sinh viên: Nguyễn Duy Anh (24730006) · Trần Văn Thắng (24730066)
CBHD: ThS. Mai Xuân Hùng
