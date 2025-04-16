**Mục tiêu:** Phân tích tài liệu (API docs, hướng dẫn thư viện/framework, đặc tả kỹ thuật, command reference) và tạo ra một "bảng tóm tắt nhanh" (cheatsheet) bằng tiếng Việt, tập trung vào các **lệnh, hàm, cú pháp, tham số và thông tin cốt lõi nhất** mà lập trình viên cần để **tham khảo cực nhanh** khi làm việc với công nghệ/ngôn ngữ/công cụ được đề cập.

**Yêu cầu chi tiết:**

1.  **Trích xuất Thông tin Lập trình Cốt lõi:**
    * Xác định và liệt kê các yếu tố quan trọng và thường dùng nhất, ví dụ:
        * **Cú pháp (Syntax) cơ bản:** Các mẫu cú pháp chính cho các cấu trúc lệnh, khai báo, v.v.
        * **Hàm/Phương thức/Lớp/Module (Functions/Methods/Classes/Modules) chủ chốt:** Liệt kê tên và mô tả *cực ngắn gọn* (1 dòng) về chức năng chính.
        * **Tham số/Đối số (Parameters/Arguments) quan trọng:** Đối với các hàm/lệnh phổ biến, liệt kê tên tham số thiết yếu, kiểu dữ liệu mong đợi, và giá trị mặc định (nếu có).
        * **Lệnh Command-Line (CLI Commands) phổ biến:** Liệt kê các lệnh thường dùng và các tùy chọn (flags/options) quan trọng nhất của chúng.
        * **Ví dụ mã nguồn (Code Snippets) cực ngắn gọn:** Chỉ bao gồm các ví dụ tối giản, minh họa trực tiếp cách sử dụng phổ biến nhất của một hàm/lệnh.
        * **Cấu hình (Configuration) thiết yếu:** Các tham số cấu hình quan trọng nhất hoặc một đoạn cấu hình mẫu tối thiểu.
        * **Kiểu dữ liệu (Data Types) hoặc cấu trúc dữ liệu (Data Structures) cốt lõi** thường xuyên sử dụng.
        * **Hằng số (Constants) hoặc giá trị mặc định (Default Values) cần nhớ.**
        * **So sánh nhanh:** Điểm khác biệt chính hoặc lựa chọn giữa các hàm/lệnh/cú pháp tương tự (nếu có và thực sự quan trọng).

2.  **Định dạng Tối ưu cho Tham khảo Lập trình:**
    * Sử dụng định dạng **cực kỳ súc tích**, ưu tiên khả năng quét nhanh (scanability). Trình bày thông tin một cách trực quan, dễ tìm.
    * Sử dụng hệ thống tiêu đề (heading) rõ ràng, đúng cấp bậc (`#`, `##`, `###`, ...).
    * **Bắt buộc sử dụng định dạng mã nguồn chuẩn:**
        * Sử dụng `inline code` (dấu backtick đơn \`) cho tất cả tên hàm, lệnh, tham số, biến, kiểu dữ liệu, tên file, giá trị chuỗi cụ thể, v.v. khi đề cập trong văn bản.
        * Sử dụng **Khối mã (Code blocks)** (dùng ba dấu backtick ```, nếu có thể hãy chỉ định ngôn ngữ, ví dụ: ```python, ```javascript, ```bash, ```sql) cho các ví dụ cú pháp nhiều dòng, cấu hình mẫu, hoặc các đoạn mã minh họa (giữ chúng thật ngắn gọn).
    * Sử dụng **bảng biểu (table)** một cách hiệu quả, ví dụ:
        * Để liệt kê: `Hàm/Lệnh` | `Mô tả cực ngắn` | `Tham số chính`
        * Để liệt kê: `Tham số/Tùy chọn` | `Kiểu/Giá trị mẫu` | `Mô tả ngắn`
        * Để so sánh nhanh các lệnh/tùy chọn.
    * Sử dụng **danh sách gạch đầu dòng (bullet points)** cho các danh sách lệnh đơn giản, các tính năng chính, hoặc các điểm lưu ý nhanh không cần bảng.

3.  **Ngôn ngữ:**
    * Sử dụng ngôn ngữ **cực kỳ ngắn gọn, đi thẳng vào vấn đề, chính xác về mặt kỹ thuật**.
    * Tập trung tối đa vào **từ khóa, tên lệnh/hàm, tên tham số, và cú pháp mẫu**. Loại bỏ gần như hoàn toàn các câu giải thích dài dòng hay văn nói.
    * Sử dụng các **thuật ngữ và viết tắt lập trình tiêu chuẩn quốc tế** (API, CLI, SDK, URL, ID, SQL, JSON, HTTP, CRUD, v.v.) một cách tự nhiên và nhất quán.

4.  **Yêu cầu Kỹ thuật:**
    * **Tuyệt đối không** bao gồm bất kỳ thẻ trích dẫn hoặc chú thích nguồn nào (ví dụ: `[cite: ...]`, `[source: ...]`).
    * Đầu ra phải là một **cheatsheet lập trình thực sự hữu ích và tiện lợi**, giúp lập trình viên tra cứu ngay lập tức các thông tin cần thiết trong quá trình code hoặc thao tác dòng lệnh. Kích thước nên cô đọng.