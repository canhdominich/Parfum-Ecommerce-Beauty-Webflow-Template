# 🚀 Hướng dẫn Deploy HTML/CSS lên Firebase Hosting

## 📋 Phần 1: Chuẩn bị

### Yêu cầu hệ thống
- ✅ Một tài khoản **Gmail** (mới hoặc có sẵn)
- ✅ **Node.js + npm** đã được cài đặt

### Kiểm tra cài đặt
```bash
node -v
npm -v
```

### Cài đặt Firebase CLI
```bash
npm install -g firebase-tools
```

### Kiểm tra phiên bản Firebase CLI
```bash
firebase --version
```

### Chuẩn bị project
Chuẩn bị folder project (ví dụ `my-site/`) chứa:
- `index.html`
- `style.css` 
- Các tài nguyên khác (images, js, etc.)

---

## 🔥 Phần 2: Tạo Project trên Firebase Console

### Các bước thực hiện
1. **Mở Firebase Console**: [console.firebase.google.com](https://console.firebase.google.com/)
2. **Tạo project mới**: 
   - Nhấn **Add project**
   - Nhập tên project (ví dụ: `my-site-demo`)
3. **Cấu hình project**:
   - Bỏ chọn **Google Analytics** nếu không cần
   - Nhấn **Create project**
4. **Hoàn tất**: Project đã sẵn sàng để kết nối từ CLI

---

## 🔐 Phần 3: Đăng nhập bằng Firebase CLI

### Thực hiện đăng nhập
```bash
firebase login
```

### Quá trình đăng nhập
1. **Trình duyệt sẽ mở tự động**
2. **Chọn tài khoản Gmail** mà bạn dùng để tạo project
3. **Nhấn Allow** để cấp quyền
4. **Kiểm tra kết quả**: Nếu đã đăng nhập, terminal sẽ hiển thị `Already logged in`

---

## ⚙️ Phần 4: Khởi tạo Firebase Hosting

### Di chuyển đến thư mục project
```bash
cd path/to/my-site
```

### Khởi tạo hosting
```bash
firebase init hosting
```

### Các bước thiết lập

| Bước | Câu hỏi | Trả lời |
|------|---------|---------|
| 1 | **Hosting: Configure files for Firebase Hosting** | ✅ Chọn (dùng mũi tên + Space + Enter) |
| 2 | **Use an existing project** | Chọn project đã tạo trên console |
| 3 | **What do you want to use as your public directory?** | `.` (nếu index.html ở thư mục hiện tại)<br/>`public` (nếu muốn dùng folder public) |
| 4 | **Configure as a single-page app?** | `n` (No) - cho HTML/CSS tĩnh |
| 5 | **Set up automatic builds and deploys with GitHub?** | `n` (No) - chưa cần CI/CD |

### Kết quả
Sau khi hoàn tất, CLI sẽ tạo:
- `firebase.json` - File cấu hình Firebase
- `.firebaserc` - File lưu thông tin project

---

## 🚀 Phần 5: Deploy lên Firebase

### Thực hiện deploy
```bash
firebase deploy
```

### Kết quả deploy
Sau khi deploy thành công, bạn sẽ thấy:
```
✅ Deploy complete!

Project Console: https://console.firebase.google.com/project/<project-id>
Hosting URL: https://<project-id>.web.app
```

### Kiểm tra website
🌐 **Mở URL hosting** để xem website đã được deploy thành công!

---

## 🔄 Phần 6: Cập nhật website

### Quy trình cập nhật
1. **Chỉnh sửa nội dung**:
   - Sửa file `index.html`
   - Cập nhật `style.css`
   - Thêm/sửa các file khác

2. **Deploy lại**:
   ```bash
   firebase deploy
   ```

3. **Kết quả**: Website sẽ được cập nhật ngay lập tức! 🎉

---

## 📄 Phần 7: Ví dụ file `firebase.json`

### Cấu hình cho thư mục gốc
Nếu bạn dùng thư mục gốc làm public (`.`):

```json
{
  "hosting": {
    "public": ".",
    "ignore": [
      "firebase.json",
      "**/.*",
      "**/node_modules/**"
    ]
  }
}
```

### Giải thích cấu hình
- `"public": "."` - Thư mục gốc làm thư mục public
- `"ignore"` - Các file/thư mục không deploy:
  - `firebase.json` - File cấu hình Firebase
  - `**/.*` - Tất cả file ẩn
  - `**/node_modules/**` - Thư mục node_modules

---

## 📝 Phần 8: Ví dụ file `index.html`

### Template HTML cơ bản
```html
<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>My Firebase Site</title>
  <link rel="stylesheet" href="style.css" />
</head>
<body>
  <h1>Xin chào! 🚀</h1>
  <p>Website này được deploy lên Firebase Hosting.</p>
</body>
</html>
```

### Các thẻ meta quan trọng
- `charset="utf-8"` - Hỗ trợ tiếng Việt
- `viewport` - Responsive design cho mobile
- `title` - Tiêu đề hiển thị trên tab browser

---

## 🎨 Phần 9: Ví dụ file `style.css`

### CSS cơ bản cho website
```css
body {
  font-family: Arial, sans-serif;
  text-align: center;
  margin: 40px;
  background-color: #f4f4f9;
  color: #333;
}

h1 { 
  color: #00796b; 
}
```

### Giải thích CSS
- `font-family` - Font chữ mặc định
- `text-align: center` - Căn giữa nội dung
- `margin: 40px` - Khoảng cách từ viền
- `background-color` - Màu nền
- `color` - Màu chữ

---

## ⚠️ Phần 10: Lỗi thường gặp & cách khắc phục

### 🔐 Lỗi đăng nhập
**Vấn đề**: Không login được hoặc sai tài khoản
```bash
firebase logout
firebase login
```

### 🎯 Lỗi chọn project
**Vấn đề**: Chọn sai project khi init
```bash
firebase use --add
```
Hoặc chạy lại: `firebase init`

### 🚫 Lỗi 404 sau deploy
**Vấn đề**: Website không hiển thị
- ✅ Kiểm tra `public` directory đã chỉ đúng thư mục chứa `index.html`
- ✅ Đảm bảo file `index.html` tồn tại

### 📁 File bị ignore
**Vấn đề**: File không được deploy
- ✅ Kiểm tra file `.firebaseignore`
- ✅ Kiểm tra mục `ignore` trong `firebase.json`

### 🔒 Lỗi quyền deploy
**Vấn đề**: Không có quyền deploy
- ✅ Gmail phải có quyền **Owner/Editor** trong project Firebase
- ✅ Kiểm tra quyền trong Firebase Console

---

## 💡 Phần 11: Lời khuyên nhanh

### 🌐 Sử dụng domain riêng
1. Vào **Firebase Console → Hosting**
2. Nhấn **Add custom domain**
3. Làm theo hướng dẫn DNS

### 🔄 Thiết lập CI/CD từ GitHub
**Cách 1**: Chọn GitHub Actions khi `firebase init`
**Cách 2**: Bật sau trong Firebase Console

### 📚 Tài liệu tham khảo
- [Firebase Hosting Documentation](https://firebase.google.com/docs/hosting)
- [Firebase CLI Reference](https://firebase.google.com/docs/cli)

---

## 🎉 Hoàn tất!

✅ **Đây là toàn bộ hướng dẫn deploy HTML/CSS lên Firebase Hosting**  
📋 **Bạn có thể copy toàn bộ nội dung này để sử dụng**

### 📞 Hỗ trợ
Nếu gặp vấn đề, hãy kiểm tra:
1. ✅ Đã cài đặt đầy đủ Node.js và Firebase CLI
2. ✅ Đã đăng nhập đúng tài khoản Firebase
3. ✅ Project đã được tạo và cấu hình đúng
4. ✅ File `index.html` tồn tại trong thư mục public

**Chúc bạn deploy thành công! 🚀**
