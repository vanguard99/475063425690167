## Bảng Hướng Dẫn Nhanh: Jailbreak iPhone 7 (iOS 15.8.3) bằng Palera1n trên Linux Mint 22 (Bao gồm Rootless & Rootful)

**Mục tiêu:** Jailbreak thiết bị để cài đặt các tinh chỉnh (tweaks) và ứng dụng không có trên App Store.

**Loại Jailbreak:** **Semi-tethered** (Cần máy tính để khởi động vào trạng thái jailbreak, nhưng có thể khởi động vào iOS gốc bình thường).

**Chọn Phương pháp Jailbreak:**

1.  **Rootless (Khuyến nghị):**
    * **Ưu điểm:** An toàn hơn, ít can thiệp hệ thống gốc, ít tốn dung lượng, tương thích tốt hơn với các biện pháp bảo mật của iOS 15+, ít bị ứng dụng phát hiện jailbreak.
    * **Nhược điểm:** Một số tweaks cũ chưa được cập nhật để tương thích.
    * **Lệnh chính:** `sudo palera1n -l` (hoặc chỉ `sudo palera1n`)
2.  **Rootful (qua fakeFS):**
    * **Ưu điểm:** Tương thích tốt hơn với các tweaks cũ được thiết kế cho cấu trúc thư mục jailbreak truyền thống.
    * **Nhược điểm:** **Cần nhiều dung lượng trống** trên iPhone (khoảng 10-15GB) để tạo bản sao hệ thống (fakeFS), tiềm ẩn rủi ro hơn Rootless, có thể ảnh hưởng hiệu năng.
    * **Lệnh chính:** `sudo palera1n -cf` (lần đầu tạo fakeFS), `sudo palera1n -f` (các lần sau boot vào fakeFS).

---

### ⚠️ Cảnh báo Quan trọng & Yêu cầu Tiên quyết (Chung cho cả hai phương pháp)

* **Rủi ro:** Việc jailbreak có thể tiềm ẩn rủi ro mất dữ liệu hoặc làm thiết bị không hoạt động đúng cách (brick). **Bạn tự chịu trách nhiệm** về mọi vấn đề xảy ra.
* **Sao lưu:** **Luôn sao lưu** dữ liệu iPhone của bạn qua iCloud hoặc Finder/iTunes trước khi bắt đầu.
* **Dung lượng (Đặc biệt cho Rootful):** Đảm bảo iPhone có đủ dung lượng trống, **ít nhất 15GB**, nếu bạn chọn phương pháp Rootful.
* **CPU Máy tính:**
    * Ưu tiên sử dụng máy tính có **CPU Intel**.
    * Máy tính dùng **CPU AMD Ryzen** có thể gặp lỗi. Nếu gặp lỗi, hãy thử với máy Intel.
    * **Không** sử dụng máy ảo (VM).
* **Cáp Kết nối:**
    * Sử dụng cáp **USB-A sang Lightning**.
    * Cáp hoặc cổng **USB-C** có thể gặp vấn đề khi vào DFU. Thử dùng USB Hub hoặc rút/cắm lại cáp nếu cần.
* **iPhone 7 (A10):** Không cần tắt mật khẩu.
* **Kết nối Internet:** Cần thiết để tải palera1n.

---

### 1. Chuẩn bị trên Linux Mint 22 (Chung cho cả hai phương pháp)

1.  **Mở Terminal:** `Ctrl+Alt+T`.
2.  **Cài đặt các gói cần thiết:**
    ```bash
    sudo apt update && sudo apt install curl libimobiledevice-utils -y
    ```
    *(Nhập mật khẩu người dùng)*

---

### 2. Cài đặt Palera1n (Chung cho cả hai phương pháp)

1.  **Tải và cài đặt Palera1n:**
    ```bash
    sudo /bin/sh -c "$(curl -fsSL https://static.palera.in/scripts/install.sh)"
    ```

---

### 3. Thực hiện Jailbreak (Chọn 1 trong 2 phương pháp dưới đây)

**Bước chuẩn bị chung (Làm trước khi chạy lệnh palera1n):**

1.  **Mở HAI cửa sổ Terminal.**
2.  **Khởi động lại dịch vụ USB:**
    * **Terminal 1:** `sudo systemctl stop usbmuxd`
    * **Terminal 1 (tiếp tục):** `sudo usbmuxd -f -p` *(Để cửa sổ này chạy)*
3.  **Kết nối iPhone** với máy tính qua cáp USB-A sang Lightning.

#### 3.A. Jailbreak theo phương pháp ROOTLESS (Khuyến nghị)

1.  **Chạy Palera1n (Rootless):**
    * **Trong Terminal 2:**
        ```bash
        sudo palera1n -l
        ```
        *(Hoặc chỉ `sudo palera1n` vì rootless là mặc định)*
2.  **Vào chế độ Recovery:** Palera1n sẽ cố gắng đưa iPhone vào Recovery.
3.  **Vào chế độ DFU:** **nhấn và giữ đồng thời nút nguồn và giảm âm lượng trong 10 giây, sau đó thả nút nguồn nhưng giữ nút giảm âm lượng thêm 5 giây** để vào DFU.
4.  **Quá trình Jailbreak:** Chờ Palera1n hoàn tất quá trình exploit và khởi động lại iPhone. Không ngắt kết nối.

#### 3.B. Jailbreak theo phương pháp ROOTFUL (fakeFS)

1.  **Chạy Palera1n (Rootful - Tạo FakeFS lần đầu):**
    * **Trong Terminal 2:**
        ```bash
        sudo palera1n -cf
        ```
        *(Cờ `-c` để tạo fakeFS, `-f` để boot vào fakeFS)*
    * **Lưu ý:** Quá trình này sẽ **lâu hơn** Rootless vì cần tạo bản sao hệ thống (~10-15GB). Đảm bảo đủ dung lượng trống.
2.  **Vào chế độ Recovery:** Palera1n sẽ cố gắng đưa iPhone vào Recovery.
3.  **Vào chế độ DFU:** **nhấn và giữ đồng thời nút nguồn và giảm âm lượng trong 10 giây, sau đó thả nút nguồn nhưng giữ nút giảm âm lượng thêm 5 giây** để vào DFU.
4.  **Quá trình Jailbreak & Tạo FakeFS:** Chờ Palera1n hoàn tất. Quá trình này bao gồm cả việc tạo fakeFS và khởi động lại iPhone. Không ngắt kết nối.
5.  **Các lần khởi động sau (Boot vào FakeFS đã tạo):** Đối với các lần khởi động lại iPhone sau này, bạn chỉ cần chạy lệnh:
    * **Trong Terminal 2:**
        ```bash
        sudo palera1n -f
        ```
    * Sau đó thực hiện lại bước vào DFU theo hướng dẫn.

---

### 4. Sau khi Jailbreak (Chung cho cả hai phương pháp)

1.  **Khởi động lại vào chế độ Jailbreak:**
    * Nếu iPhone khởi động lại hoàn toàn, bạn cần kết nối lại với máy tính và chạy lại lệnh Palera1n tương ứng với phương pháp đã chọn để kích hoạt lại jailbreak:
        * **Rootless:** `sudo palera1n -l` (hoặc `sudo palera1n`) rồi vào DFU.
        * **Rootful:** `sudo palera1n -f` rồi vào DFU.
2.  **Cài đặt Trình quản lý Gói:**
    * Mở ứng dụng **Palera1n Loader** trên iPhone.
    * Nhấn vào **Sileo** (hoặc Zebra) và chọn **Install**.
    * Dùng Sileo/Zebra để cài đặt tweaks.

---

### 5. Khắc phục sự cố và Quản lý

* **Lỗi CPU AMD Ryzen/USB-C:** Xem phần cảnh báo.
* **Không vào được DFU:** Kiểm tra cáp, cổng USB, làm đúng hướng dẫn thời gian nhấn nút.
* **Gỡ bỏ Jailbreak hoàn toàn:**
    ```bash
    sudo palera1n --force-revert
    ```
    *(Lệnh này sẽ cố gắng xóa bỏ các thay đổi của jailbreak)*
* **Xóa FakeFS (Chỉ dành cho Rootful):** Nếu bạn muốn xóa phân vùng fakeFS (giải phóng dung lượng) và quay lại dùng Rootless hoặc gỡ jailbreak:
    ```bash
    sudo palera1n -C
    ```
    *(Hoặc `sudo palera1n --clean-fakefs`)*
