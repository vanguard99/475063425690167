# Bảng Tổng Hợp Mẹo và Thủ Thuật ADB (Android Debug Bridge)

## I. Cài Đặt và Kết Nối

### 1. Chuẩn Bị Trên Điện Thoại Android

1.  **Bật Tùy chọn nhà phát triển:**
    * Mở `Cài đặt` > `Thông tin điện thoại` (hoặc `Giới thiệu về điện thoại`).
    * Nhấn liên tục **7 lần** vào mục `Số bản dựng` (hoặc `Số hiệu bản tạo`/`Build number`) cho đến khi có thông báo bạn đã là nhà phát triển.
    * *Lưu ý:* Vị trí `Số bản dựng` có thể khác nhau tùy hãng điện thoại.
2.  **Bật Gỡ lỗi USB (USB Debugging):**
    * Quay lại `Cài đặt`, tìm mục `Tùy chọn nhà phát triển` mới xuất hiện (thường nằm trong `Cài đặt` > `Hệ thống` hoặc `Cài đặt bổ sung`).
    * Vào `Tùy chọn nhà phát triển`, tìm và **bật** tùy chọn `Gỡ lỗi USB`.
3.  **Kết Nối và Ủy Quyền:**
    * Sử dụng cáp USB tốt để kết nối điện thoại với máy tính.
    * Kiểm tra màn hình điện thoại. Nếu có hộp thoại hỏi "Cho phép gỡ lỗi USB?", hãy nhấn `Cho phép` / `Allow`.
    * *Nên:* Đánh dấu vào ô "Luôn cho phép từ máy tính này" để không phải xác nhận lại trong các lần kết nối sau.

### 2. Cài Đặt ADB Trên Máy Tính

* **Tải Công Cụ:**
    1.  Truy cập trang chính thức: `https://developer.android.com/studio/releases/platform-tools`
    2.  Tải xuống gói "SDK Platform-Tools" phù hợp với hệ điều hành của bạn (Windows, macOS, Linux).
* **Giải Nén:**
    1.  Giải nén tệp ZIP vừa tải vào một thư mục dễ truy cập (ví dụ: `C:\platform-tools` trên Windows, `/Users/ten_ban/platform-tools` trên macOS, `/home/ten_ban/platform-tools` trên Linux).
* **Thêm Thư Mục ADB vào Biến Môi Trường PATH (Quan trọng):**
    * **Windows:**
        1.  Tìm kiếm "Environment Variables" trong Start Menu, chọn `Edit the system environment variables`.
        2.  Trong cửa sổ System Properties, chọn `Environment Variables...`.
        3.  Trong phần `System variables` (hoặc `User variables` nếu chỉ muốn dùng cho tài khoản của bạn), tìm và chọn biến `Path`, sau đó nhấn `Edit...`.
        4.  Nhấn `New` và dán đường dẫn đầy đủ đến thư mục `platform-tools` bạn vừa giải nén (ví dụ: `C:\platform-tools`).
        5.  Nhấn `OK` trên tất cả các cửa sổ.
    * **macOS/Linux:**
        1.  Mở Terminal.
        2.  Chỉnh sửa tệp cấu hình shell của bạn (`.zshrc` cho Zsh, `.bashrc` hoặc `.bash_profile` cho Bash) bằng lệnh `nano ~/.zshrc` (hoặc tệp tương ứng).
        3.  Thêm dòng sau vào cuối tệp (thay `/duong/dan/toi/platform-tools` bằng đường dẫn thực tế):
            ```bash
            export PATH="/duong/dan/toi/platform-tools:$PATH"
            ```
        4.  Lưu tệp (Ctrl+O trong nano, sau đó Enter) và thoát (Ctrl+X).
        5.  Áp dụng thay đổi bằng lệnh `source ~/.zshrc` (hoặc tệp tương ứng).
    * **macOS (Cách khác dùng Homebrew):**
        1.  Mở Terminal.
        2.  Chạy lệnh: `brew install --cask android-platform-tools`
* **Kiểm Tra Cài Đặt:**
    1.  **Mở một cửa sổ Terminal/Command Prompt/PowerShell MỚI.**
    2.  Gõ lệnh: `adb version`
    3.  Nếu hiển thị thông tin phiên bản (ví dụ: "Android Debug Bridge version...") là thành công.

### 3. Kiểm Tra Kết Nối Điện Thoại

1.  Đảm bảo điện thoại đã kết nối với máy tính qua USB và đã bật Gỡ lỗi USB, đã được Ủy quyền.
2.  Mở Terminal/CMD/PowerShell.
3.  Gõ lệnh: `adb devices`
4.  **Kết quả mong đợi:** Hiển thị một dòng với số serial của thiết bị và trạng thái `device`.
    * Nếu hiển thị `unauthorized`: Kiểm tra lại màn hình điện thoại để cấp quyền.
    * Nếu không hiển thị gì hoặc `offline`: Kiểm tra cáp, cổng USB, driver (nếu cần trên Windows cũ), và đảm bảo đã bật Gỡ lỗi USB.

## II. Lệnh ADB Cơ Bản (Chạy từ Máy Tính)

* `adb devices`
    * **Mục đích:** Liệt kê các thiết bị Android đang kết nối và trạng thái của chúng.
* `adb shell`
    * **Mục đích:** Mở một giao diện dòng lệnh (shell) tương tác trực tiếp trên điện thoại. Sau khi chạy lệnh này, bạn có thể gõ các lệnh Linux chuẩn (xem Phần III).
    * **Thoát:** Gõ `exit` hoặc nhấn `Ctrl+D`.
* `adb push <đường_dẫn_trên_máy_tính> <đường_dẫn_trên_điện_thoại>`
    * **Mục đích:** Sao chép tệp hoặc thư mục từ máy tính vào điện thoại.
    * **Ví dụ:** `adb push C:\hinhanh.jpg /sdcard/Pictures/`
    * *Lưu ý:* Đường dẫn trên điện thoại thường bắt đầu bằng `/sdcard/` (bộ nhớ trong) hoặc các đường dẫn hệ thống khác nếu có quyền.
* `adb pull <đường_dẫn_trên_điện_thoại> [đường_dẫn_trên_máy_tính]`
    * **Mục đích:** Sao chép tệp hoặc thư mục từ điện thoại về máy tính.
    * **Ví dụ:** `adb pull /sdcard/DCIM/Camera/anh_moi.jpg C:\Users\Ban\Desktop\`
    * *Lưu ý:* Nếu bỏ qua [đường_dẫn_trên_máy_tính], tệp sẽ được lưu vào thư mục hiện tại trên máy tính.
* `adb install <đường_dẫn_đến_file_APK_trên_máy_tính>`
    * **Mục đích:** Cài đặt ứng dụng từ tệp APK trên máy tính vào điện thoại.
    * **Ví dụ:** `adb install C:\Downloads\myapp.apk`
    * *Lưu ý:* Có thể thêm cờ `-r` để cài đặt lại ứng dụng đã có (`adb install -r ...`).
* `adb uninstall <tên_gói_ứng_dụng>`
    * **Mục đích:** Gỡ cài đặt một ứng dụng khỏi điện thoại.
    * **Ví dụ:** `adb uninstall com.facebook.katana`
    * *Lưu ý:* Cần biết tên gói (package name) của ứng dụng. Xem cách tìm ở Phần III.
* `adb logcat`
    * **Mục đích:** Hiển thị log hệ thống Android theo thời gian thực (hữu ích cho việc gỡ lỗi).
    * **Dừng lại:** Nhấn `Ctrl+C`.
    * *Lưu ý:* Có thể lọc log với các tùy chọn nâng cao (`adb logcat *:E` chỉ hiển thị lỗi, `adb logcat -s TenTag` lọc theo tag).
* `adb reboot`
    * **Mục đích:** Khởi động lại điện thoại.
    * *Cảnh báo:* Đảm bảo không có thao tác quan trọng đang diễn ra.
* `adb reboot bootloader`
    * **Mục đích:** Khởi động lại điện thoại vào chế độ Bootloader/Fastboot.
* `adb reboot recovery`
    * **Mục đích:** Khởi động lại điện thoại vào chế độ Recovery.
* `adb shell <lệnh_shell>`
    * **Mục đích:** Chạy một lệnh shell duy nhất trên điện thoại mà không cần vào shell tương tác.
    * **Ví dụ:** `adb shell wm size`

## III. Lệnh Shell Thường Dùng (Gõ sau khi đã vào `adb shell` hoặc dùng `adb shell <lệnh>`)

* **Quản lý ứng dụng (Package Manager - `pm`)**
    * `pm list packages` : Liệt kê tất cả tên gói ứng dụng đã cài đặt.
    * `pm list packages -s` : Chỉ liệt kê các gói hệ thống.
    * `pm list packages -3` : Chỉ liệt kê các gói do người dùng cài (không phải hệ thống).
    * `pm list packages -d` : Chỉ liệt kê các gói đã bị vô hiệu hóa.
    * `pm list packages -e` : Chỉ liệt kê các gói đang được bật.
    * *Tìm kiếm (Chạy từ PC):*
        * `adb shell pm list packages | grep <từ_khóa>` (Trên macOS/Linux/PowerShell)
        * `adb shell pm list packages | findstr <từ_khóa>` (Trên Windows CMD)
        * **Ví dụ:** `adb shell pm list packages | grep facebook`
    * `pm path <tên_gói>` : Hiển thị đường dẫn đến tệp APK của ứng dụng.
        * **Ví dụ:** `pm path com.google.android.youtube`
    * `pm clear <tên_gói>` : Xóa toàn bộ dữ liệu (cache, cài đặt) của ứng dụng.
        * *Cảnh báo:* Thao tác này giống như cài lại ứng dụng, mất hết dữ liệu đăng nhập, cài đặt riêng.
    * `pm enable <tên_gói>` : Bật lại một ứng dụng đã bị vô hiệu hóa.
    * `pm disable-user --user 0 <tên_gói>` : Vô hiệu hóa một ứng dụng cho người dùng hiện tại (thường dùng để ẩn bloatware không cần root). Ứng dụng vẫn còn trên hệ thống.
    * `pm uninstall -k --user 0 <tên_gói>` : Gỡ cài đặt ứng dụng cho người dùng hiện tại nhưng giữ lại dữ liệu và cache (thường dùng để gỡ bloatware không cần root).
        * *Cảnh báo:* Đây không phải là gỡ cài đặt hoàn toàn. Ứng dụng có thể quay lại sau khi cập nhật hệ thống hoặc khôi phục cài đặt gốc.
* **Thông tin màn hình (Window Manager - `wm`)**
    * `wm size` : Hiển thị độ phân giải màn hình vật lý (ví dụ: `Physical size: 1080x2400`).
    * `wm density` : Hiển thị mật độ điểm ảnh vật lý (DPI) của màn hình (ví dụ: `Physical density: 420`).
* **Mô phỏng thao tác người dùng (`input`)**
    * `input keyevent <mã_phím>` : Gửi một sự kiện nhấn phím.
        * **Ví dụ:** `input keyevent 3` (Phím Home), `input keyevent 4` (Phím Back), `input keyevent 26` (Phím Nguồn), `input keyevent 66` (Phím Enter).
        * *Lưu ý:* Tìm danh sách mã phím đầy đủ bằng cách tìm kiếm "Android keyevent codes".
    * `input text "<văn_bản>"` : Nhập văn bản vào ô nhập liệu đang được focus.
        * **Ví dụ:** `input text "Xin chao"`
        * *Lưu ý:* Đặt văn bản trong dấu ngoặc kép. Để nhập dấu cách, dùng `%s`. Ví dụ: `input text "Xin%schao"`
    * `input tap <x> <y>` : Mô phỏng một lần chạm vào tọa độ (x, y) trên màn hình.
    * `input swipe <x1> <y1> <x2> <y2> [thời_gian_ms]` : Mô phỏng thao tác vuốt từ (x1, y1) đến (x2, y2) trong khoảng thời gian (mili giây).
* **Chụp ảnh & Quay màn hình**
    * `screencap /sdcard/screenshot.png` : Chụp ảnh màn hình và lưu vào đường dẫn `/sdcard/screenshot.png` trên điện thoại.
    * *Lấy về máy tính:* `adb pull /sdcard/screenshot.png`
    * `screenrecord /sdcard/video.mp4` : Quay video màn hình và lưu vào `/sdcard/video.mp4`.
    * *Dừng quay:* Nhấn `Ctrl+C` trong cửa sổ Terminal/CMD đang chạy lệnh.
    * *Giới hạn thời gian:* `screenrecord --time-limit 10 /sdcard/video10s.mp4` (quay trong 10 giây). Mặc định là 3 phút.
    * *Lấy về máy tính:* `adb pull /sdcard/video.mp4`

## IV. Lệnh Shell Nâng Cao (Sử dụng cẩn thận)

* **Xem/Thay đổi Cài đặt Hệ thống (`settings`)**
    * `settings list system` : Liệt kê các cài đặt trong bảng `system`.
    * `settings list secure` : Liệt kê các cài đặt trong bảng `secure`.
    * `settings list global` : Liệt kê các cài đặt trong bảng `global`.
    * `settings get <bảng> <tên_cài_đặt>` : Xem giá trị của một cài đặt cụ thể.
        * **Ví dụ:** `settings get system screen_brightness`
    * `settings put <bảng> <tên_cài_đặt> <giá_trị>` : Thay đổi giá trị của một cài đặt.
        * *Cảnh báo:* Thay đổi cài đặt không đúng có thể gây lỗi hệ thống. Chỉ thực hiện nếu bạn biết rõ mình đang làm gì. Sao lưu dữ liệu trước khi thay đổi cài đặt quan trọng.
* **Thông tin chi tiết hệ thống (`dumpsys`)**
    * `dumpsys <tên_dịch_vụ>` : Hiển thị thông tin trạng thái chi tiết của một dịch vụ hệ thống.
    * **Ví dụ:** `dumpsys battery` (thông tin pin), `dumpsys activity` (thông tin activity), `dumpsys package` (thông tin các gói), `dumpsys meminfo <tên_gói>` (thông tin bộ nhớ của ứng dụng).
    * *Lưu ý:* Kết quả trả về thường rất dài và chi tiết, cần biết cách lọc hoặc tìm kiếm thông tin cần thiết.
* **Thuộc tính hệ thống (`getprop`, `setprop`)**
    * `getprop` : Hiển thị danh sách các thuộc tính hệ thống (thường chỉ đọc).
    * `getprop <tên_thuộc_tính>` : Hiển thị giá trị của một thuộc tính cụ thể.
    * `setprop <tên_thuộc_tính> <giá_trị>` : Thay đổi giá trị thuộc tính (thường yêu cầu quyền root và có thể không bền vững sau khi khởi động lại).
        * *Cảnh báo:* Rất nguy hiểm nếu không hiểu rõ.