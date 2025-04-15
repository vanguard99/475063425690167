**Cheatsheet: Cloudflare WARP trên Linux Mint**

**Mục tiêu:** Cung cấp bản tóm tắt các lệnh và bước chính để cài đặt, sử dụng và gỡ bỏ Cloudflare WARP trên Linux Mint một cách nhanh chóng.

**WARP là gì?** Dịch vụ VPN (thường được gọi là VPN nhưng hoạt động hơi khác) miễn phí từ Cloudflare, giúp tăng cường bảo mật và có thể cải thiện tốc độ kết nối Internet bằng cách định tuyến lưu lượng truy cập qua mạng của Cloudflare.

**1. Chuẩn Bị Cài Đặt**

* **Xác định codename Ubuntu của Linux Mint:**
    ```bash
    cat /etc/os-release | grep UBUNTU_CODENAME
    ```
    * `jammy`: Linux Mint 21.x
    * `focal`: Linux Mint 20.x
    * `noble`: Linux Mint 22.x (Nếu chưa hỗ trợ chính thức, có thể thử dùng `jammy`)
    * *Lý do:* Cần codename để thêm đúng kho lưu trữ phần mềm (repository).

**2. Cài Đặt WARP**

* **Thêm Khóa GPG của Cloudflare:**
    ```bash
    curl -fsSL https://pkg.cloudflareclient.com/pubkey.gpg | sudo gpg --dearmor -o /usr/share/keyrings/cloudflare-warp-archive-keyring.gpg
    ```
* **Thêm Kho Lưu Trữ Cloudflare:** (Thay `jammy` bằng codename bạn tìm được ở Bước 1 nếu cần)
    ```bash
    echo "deb [signed-by=/usr/share/keyrings/cloudflare-warp-archive-keyring.gpg] https://pkg.cloudflareclient.com/ jammy main" | sudo tee /etc/apt/sources.list.d/cloudflare-client.list
    ```
* **Cập nhật Danh sách Gói và Cài đặt WARP:**
    ```bash
    sudo apt update && sudo apt install cloudflare-warp -y
    ```

**3. Thiết Lập và Sử Dụng**

* **Khởi động & Kiểm tra Dịch vụ WARP:**
    ```bash
    # Khởi động lại nếu cần
    sudo systemctl restart warp-svc
    # Kiểm tra trạng thái (phải là active/running)
    sudo systemctl status warp-svc
    # Khởi động nếu chưa chạy
    sudo systemctl start warp-svc
    ```
* **Đăng ký Thiết bị (Lần đầu tiên):**
    ```bash
    warp-cli registration new
    ```
* **Kết nối WARP:**
    ```bash
    warp-cli connect
    ```
* **Kiểm tra Trạng thái Kết nối:**
    ```bash
    warp-cli status
    ```
    * Tìm dòng `Status: Connected` để xác nhận.
* **Kiểm tra Địa chỉ IP Public (Xác nhận WARP hoạt động):**
    ```bash
    curl ifconfig.me
    # Hoặc
    curl https://www.cloudflare.com/cdn-cgi/trace | grep ip=
    ```
    * Địa chỉ IP hiển thị phải khác với IP gốc của bạn và thuộc về Cloudflare.
* **Ngắt Kết nối WARP:**
    ```bash
    warp-cli disconnect
    ```

**4. Gỡ Cài Đặt WARP**

* **(Tùy chọn, nên làm) Xóa Đăng ký & Cấu hình:**
    ```bash
    sudo warp-cli delete-all
    ```
* **Gỡ bỏ Gói Phần mềm và Cấu hình:**
    ```bash
    sudo apt remove --purge cloudflare-warp -y
    ```
* **(Tùy chọn) Xóa Tệp Kho Lưu Trữ:**
    ```bash
    sudo rm /etc/apt/sources.list.d/cloudflare-client.list
    ```
* **(Tùy chọn) Xóa Khóa GPG:**
    ```bash
    sudo rm /usr/share/keyrings/cloudflare-warp-archive-keyring.gpg
    ```
* **Cập nhật lại Danh sách Gói:**
    ```bash
    sudo apt update
    ```

**5. Khắc Phục Lỗi Phổ Biến**

* **Lỗi "Registration Missing" hoặc Không kết nối được:**
    1.  `sudo systemctl restart warp-svc`
    2.  `warp-cli registration new` (Thử đăng ký lại)
    3.  `warp-cli connect`
* **Không thể `apt update` sau khi thêm kho:**
    * Kiểm tra lại kết nối mạng.
    * Kiểm tra xem codename trong tệp `/etc/apt/sources.list.d/cloudflare-client.list` có chính xác không.
    * Đảm bảo đã thêm khóa GPG đúng cách.