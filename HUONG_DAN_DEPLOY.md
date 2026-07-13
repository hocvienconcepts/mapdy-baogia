# Hướng dẫn đưa trang Báo giá Mapdy (v1.18) lên Cloudflare Pages qua GitHub

Mục tiêu: trang `index.html` chạy được tại địa chỉ dạng `https://ten-ban-chon.pages.dev`,
và mỗi lần sửa file trên GitHub, Cloudflare tự cập nhật lại trang.

Thư mục cần đưa lên: **`mapdy-baogia-v2-web`** (chứa `index.html`, `README.md`, `.gitignore`).

---

## PHẦN 1 — Đưa file lên GitHub

### Cách A — Tải lên bằng trình duyệt (không cần cài đặt) ✅ khuyên dùng

1. Vào https://github.com → đăng nhập (chưa có thì **Sign up** tạo tài khoản miễn phí).
2. Góc trên bên phải bấm **➕ → New repository**.
3. Đặt:
   - **Repository name:** `mapdy-baogia-v2` (tên bất kỳ, không dấu, không khoảng trắng).
   - Chọn **Public**.
   - **KHÔNG** tick "Add a README".
   - Bấm **Create repository**.
4. Ở repo trống, bấm **"uploading an existing file"** (hoặc **Add file → Upload files**).
5. Mở thư mục `mapdy-baogia-v2-web`, **kéo cả 3 file** (`index.html`, `README.md`, `.gitignore`) thả vào.
   > `index.html` phải nằm ở **gốc repo**, không nằm trong folder con.
6. Bấm **Commit changes**.

### Cách B — Dùng git trên máy (nếu quen dòng lệnh)

Mở Terminal/Git Bash tại thư mục `mapdy-baogia-v2-web`:

```bash
git init
git add .
git commit -m "Mapdy bao gia Founder v1.18"
git branch -M main
git remote add origin https://github.com/<TEN_GITHUB>/mapdy-baogia-v2.git
git push -u origin main
```

---

## PHẦN 2 — Nối GitHub với Cloudflare Pages

1. Vào https://dash.cloudflare.com → đăng nhập (đăng ký miễn phí nếu chưa có).
2. Menu trái: **Workers & Pages** → **Create** → tab **Pages** → **Connect to Git**.
3. **Connect GitHub**, cho phép truy cập, chọn repo `mapdy-baogia-v2`.
4. Cấu hình build để **mặc định**:
   - **Framework preset:** None
   - **Build command:** *(để trống)*
   - **Build output directory:** `/`
5. Bấm **Save and Deploy**, đợi ~30–60 giây.
6. Nhận link dạng: `https://mapdy-baogia-v2.pages.dev`

---

## PHẦN 3 — Đổi subdomain / tên miền riêng (tuỳ chọn)

- Tên `.pages.dev` lấy theo **Project name** (mặc định = tên repo). Muốn tên khác thì đặt Project name khi tạo.
- Tên miền riêng (vd `baogia.mapdy.vn`): project Pages → **Custom domains** → **Set up a custom domain** → trỏ DNS theo hướng dẫn.

---

## Cập nhật về sau
Sửa `index.html` trên GitHub (file → ✏️ Edit, hoặc `git push`). Cloudflare **tự build lại** trong ~1 phút.

## Lỗi thường gặp
| Hiện tượng | Xử lý |
|---|---|
| Link `.pages.dev` báo 404 | `index.html` không ở gốc repo — kiểm tra lại vị trí file. |
| Cloudflare không thấy repo | Repo để Private chưa cấp quyền — đổi Public hoặc cấp quyền repo cho Cloudflare. |
| Sửa xong chưa đổi | Đợi 1–2 phút; Ctrl/Cmd + Shift + R để xoá cache. |
