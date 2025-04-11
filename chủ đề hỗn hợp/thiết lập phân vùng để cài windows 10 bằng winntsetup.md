**Bước 1: Xóa các phân vùng**
- Chọn ổ cứng cần thao tác  
- Nhấp chuột phải → chọn **"Delete All Partitions"** → chọn **"Yes"** để xác nhận.

**Bước 2: Chuyển sang định dạng GPT**
- Nhấp chuột phải vào ổ cứng → chọn **"Convert GPT Disk"** → chọn **"Yes"** để xác nhận.

**Bước 3: Tạo phân vùng EFI (định dạng FAT32)**
- Nhấp chuột phải vào vùng dung lượng trống → chọn **"Create Partition"**  
  - **File System:** FAT32  
  - **Partition Size:** 100MB

**Bước 4: Đặt phân vùng EFI**
- Chọn phân vùng EFI mới tạo → nhấp chuột phải → chọn **"Set as EFI System Partition"**  
- Nhấp **"OK"** để xác nhận.

**Bước 5: Tạo phân vùng cài Windows**
- Nhấp chuột phải vào vùng dung lượng trống còn lại → chọn **"Create Partition"**  
  - **Label:** Windows  
  - **File System:** NTFS  
  - **Partition Size:** dùng toàn bộ dung lượng trống còn lại.

**Bước 6: Áp dụng các thay đổi**
- Nhấn **"Apply"** → chọn **"Yes"** để bắt đầu tiến trình.

**Bước 7: Kết quả sau khi hoàn tất**

| Phân vùng   | Mục đích                        |
| ----------- | ------------------------------- |
| EFI (100MB) | Dùng để khởi động hệ thống UEFI |
| NTFS        | Dùng để cài đặt Windows         |