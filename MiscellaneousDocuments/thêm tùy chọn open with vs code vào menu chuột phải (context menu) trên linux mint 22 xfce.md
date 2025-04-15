thêm tùy chọn **"Open with VS Code"** vào **menu chuột phải (context menu)** trên **Linux Mint 22 XFCE**.

---

## Mục tiêu:
- Thêm tùy chọn **"Open with VS Code"** khi **chuột phải vào file hoặc thư mục** trong **Thunar (trình quản lý tệp của XFCE)**.

---

## ✅ Bước 1: Mở **Thunar Custom Actions**
Mở terminal và chạy:
```bash
thunar -q && thunar
```
Sau đó vào:
- **Edit → Configure custom actions…**

---

## ✅ Bước 2: Thêm custom action "Open with VS Code"
Trong cửa sổ **Custom Actions**, làm theo các bước:

### 1. Nhấn **"+"** để thêm action mới.

### 2. Điền các thông tin như sau:

- **Name:** Open with VS Code  
- **Description:** Mở bằng Visual Studio Code  
- **Command:**  
```bash
code %F
```

> `%F` sẽ nhận nhiều file hoặc folder.

- **Icon:** Chọn biểu tượng VS Code nếu thích (thường nằm trong `/usr/share/pixmaps/code.png`)

---

## ✅ Bước 3: Thẻ **"Appearance Conditions"**
Chọn:
- **File Pattern:** `*`
- **Range (min-max):** `*`
- **Appears if selection contains:** ✔ Directories** ✔ Other files

> Giúp bạn mở bất cứ file hoặc folder nào với VS Code.