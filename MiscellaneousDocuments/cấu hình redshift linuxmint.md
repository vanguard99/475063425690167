#  Hướng Dẫn Cài Đặt & Cấu Hình Redshift trên Linux Mint

Redshift giúp bảo vệ mắt bằng cách điều chỉnh nhiệt độ màu màn hình theo thời gian trong ngày. Dưới đây là hướng dẫn chi tiết để cài đặt và thiết lập Redshift tự động chạy khi khởi động.

---

## 1. Cài Đặt Redshift

Mở Terminal và chạy lần lượt các lệnh sau:
```bash
sudo apt update
sudo apt install redshift redshift-gtk
```

---

## 2. Kiểm Tra Cài Đặt

Xác nhận Redshift đã được cài bằng lệnh:
```bash
redshift -h
```

Nếu thấy thông tin trợ giúp hiện ra là OK.

---

## 3. Chạy Redshift Thủ Công

Để giảm ánh sáng xanh và làm dịu mắt vào ban đêm, bạn có thể thủ công thiết lập nhiệt độ màu như sau:
```bash
redshift -O 3500
```

> 3500K là mức màu vàng ấm phù hợp buổi tối. Có thể thay đổi theo sở thích.

---

## 4. Tự Động Chạy Khi Khởi Động

Thiết lập để Redshift tự động chạy khi khởi động máy:

1. Vào **Menu > Settings > Session and Startup**  
2. Chọn tab **Application Autostart**, nhấn **Add**  
3. Điền thông tin:

   - **Name:** Redshift  
   - **Description:** Chạy Redshift ở 3500K  
   - **Command:**  
     ```bash
     sh -c 'sleep 10 && redshift -O 3500 &'
     ```

4. Nhấn **OK** để lưu.

> Dòng `sleep 10` giúp đợi hệ thống ổn định trước khi chạy Redshift.

---

## 5.  Khôi Phục Màu Mặc Định

Khi muốn đưa màn hình về nhiệt độ màu tiêu chuẩn (6500K):
```bash
redshift -x
```