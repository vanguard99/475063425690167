**Cheatsheet Vòng lặp Java**

**1. Vòng lặp `for`**

* **Mục đích:** Thường dùng khi biết trước số lần lặp hoặc cần kiểm soát biến đếm chặt chẽ.
* **Cú pháp:**
    ```java
    for (khởi_tạo; điều_kiện_tiếp_tục; cập_nhật) {
        // Khối lệnh lặp lại
    }
    ```
    * `khởi_tạo`: Thực thi 1 lần duy nhất khi bắt đầu (vd: `int i = 0;`).
    * `điều_kiện_tiếp_tục`: Biểu thức `boolean`, kiểm tra *trước* mỗi lần lặp (vd: `i < 10`). Nếu `false`, vòng lặp kết thúc.
    * `cập_nhật`: Thực thi *sau* mỗi lần lặp (vd: `i++`, `i += 2`).
* **Ví dụ cơ bản (In số từ 0 đến 4):**
    ```java
    for (int i = 0; i < 5; i++) {
        System.out.println("i = " + i);
    }
    ```
* **Ví dụ duyệt mảng (Array):**
    ```java
    int[] numbers = {10, 20, 30};
    for (int i = 0; i < numbers.length; i++) {
        System.out.println("Phần tử tại index " + i + ": " + numbers[i]);
    }
    ```
* **Biến thể:** Có thể có nhiều biểu thức khởi tạo/cập nhật (cách nhau bởi `,`), hoặc bỏ trống các phần (vẫn giữ `;`).
    ```java
    for (int i = 0, j = 5; i < j; i++, j--) { /* ... */ }
    int k = 0;
    for (; k < 3; ) { /*...*/ k++; } // Khởi tạo ngoài, cập nhật trong
    // for (;;) { /* Vòng lặp vô hạn */ }
    ```
* **Phạm vi biến:** Biến khai báo trong phần `khởi_tạo` chỉ tồn tại bên trong vòng lặp.

**2. Vòng lặp `while`**

* **Mục đích:** Dùng khi số lần lặp không xác định trước, phụ thuộc vào điều kiện, và khối lệnh có thể không thực thi lần nào.
* **Cú pháp:**
    ```java
    while (điều_kiện_tiếp_tục) {
        // Khối lệnh lặp lại
        // Cần có lệnh thay đổi điều_kiện_tiếp_tục để tránh lặp vô hạn
    }
    ```
    * `điều_kiện_tiếp_tục`: Biểu thức `boolean`, kiểm tra *trước* mỗi lần lặp.
* **Đặc điểm:** Kiểm tra trước (pre-test loop).
* **Ví dụ (Đếm ngược từ 3 về 1):**
    ```java
    int count = 3;
    while (count > 0) {
        System.out.println(count);
        count--; // Cập nhật biến điều kiện
    }
    ```
* **Ví dụ (Đọc đến khi nhập giá trị sentinel):**
    ```java
    Scanner scanner = new Scanner(System.in);
    int input;
    System.out.print("Nhập số (-1 để dừng): ");
    input = scanner.nextInt(); // Đọc lần đầu
    while (input != -1) {
        // Xử lý input
        System.out.print("Nhập số tiếp theo (-1 để dừng): ");
        input = scanner.nextInt(); // Đọc lần tiếp theo
    }
    scanner.close();
    ```

**3. Vòng lặp `do-while`**

* **Mục đích:** Tương tự `while`, nhưng đảm bảo khối lệnh thực thi *ít nhất một lần*. Thích hợp cho menu, yêu cầu nhập liệu lần đầu.
* **Cú pháp:**
    ```java
    do {
        // Khối lệnh lặp lại
        // Cần có lệnh thay đổi điều_kiện_tiếp_tục
    } while (điều_kiện_tiếp_tục); // Lưu ý dấu ; ở cuối
    ```
    * `điều_kiện_tiếp_tục`: Biểu thức `boolean`, kiểm tra *sau* mỗi lần lặp.
* **Đặc điểm:** Kiểm tra sau (post-test loop).
* **Ví dụ (Menu đơn giản):**
    ```java
    Scanner scanner = new Scanner(System.in);
    int choice;
    do {
        System.out.println("1. Option A");
        System.out.println("0. Exit");
        System.out.print("Chọn: ");
        choice = scanner.nextInt();
        // Xử lý choice...
    } while (choice != 0);
    scanner.close();
    ```

**4. Vòng lặp `for-each` (Enhanced for loop)**

* **Mục đích:** Duyệt tuần tự qua tất cả phần tử của mảng hoặc collection (`Iterable`) một cách đơn giản, dễ đọc.
* **Cú pháp:**
    ```java
    for (Kiểu_Phần_Tử tên_biến_tạm : nguồn_dữ_liệu) {
        // Sử dụng tên_biến_tạm để truy cập phần tử hiện tại
    }
    ```
    * `nguồn_dữ_liệu`: Mảng hoặc đối tượng cài đặt `Iterable`.
* **Ví dụ (Duyệt `ArrayList`):**
    ```java
    List<String> names = new ArrayList<>();
    names.add("Alice");
    names.add("Bob");
    for (String name : names) {
        System.out.println(name);
    }
    ```
* **Ví dụ (Duyệt mảng `int`):**
    ```java
    int[] scores = {9, 8, 10};
    int total = 0;
    for (int score : scores) {
        total += score;
    }
    System.out.println("Tổng điểm: " + total);
    ```
* **Ưu điểm:** Ngắn gọn, dễ đọc, ít lỗi chỉ số.
* **Hạn chế:**
    * Chỉ duyệt tới, không có chỉ số (index).
    * Không thể sửa đổi cấu trúc collection khi đang duyệt (thường gây `ConcurrentModificationException`).
    * Gán giá trị mới cho `tên_biến_tạm` không thay đổi phần tử gốc trong nguồn (trừ khi gọi phương thức thay đổi trạng thái của đối tượng tham chiếu).

**5. Lệnh Điều khiển Vòng lặp**

* **`break;`**: Thoát *ngay lập tức* khỏi vòng lặp (`for`, `while`, `do-while`) hoặc `switch` chứa nó.
    ```java
    for (int i = 0; i < 10; i++) {
        if (i == 5) {
            break; // Dừng vòng lặp khi i = 5
        }
        System.out.print(i + " "); // Chỉ in 0 1 2 3 4
    }
    ```
* **`continue;`**: Bỏ qua phần còn lại của lần lặp *hiện tại* và chuyển sang lần lặp tiếp theo.
    ```java
    for (int i = 0; i < 5; i++) {
        if (i % 2 == 0) { // Nếu i chẵn
            continue; // Bỏ qua phần còn lại, sang lần lặp kế tiếp
        }
        System.out.print(i + " "); // Chỉ in số lẻ: 1 3
    }
    ```
* **Nhãn (Labels) với `break` và `continue` (Ít dùng):** Cho phép `break` hoặc `continue` khỏi vòng lặp lồng nhau cụ thể.
    ```java
    outerLoop: // Nhãn
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            if (i * j > 2) {
                System.out.println("Breaking outer loop at i=" + i + ", j=" + j);
                break outerLoop; // Thoát vòng lặp có nhãn outerLoop
            }
            if (i == 1 && j == 1) {
                 System.out.println("Continuing outer loop at i=" + i + ", j=" + j);
                 continue outerLoop; // Bỏ qua phần còn lại của i=1, sang i=2
            }
            System.out.println(" i=" + i + ", j=" + j);
        }
    }
    ```

**6. Vòng lặp Lồng nhau (Nested Loops)**

* Đặt một vòng lặp bên trong vòng lặp khác. Vòng trong hoàn thành tất cả các lần lặp của nó cho *mỗi* lần lặp của vòng ngoài.
* **Ví dụ (In ma trận 2x3):**
    ```java
    int[][] matrix = {{1, 2, 3}, {4, 5, 6}};
    for (int i = 0; i < matrix.length; i++) { // Duyệt hàng
        for (int j = 0; j < matrix[i].length; j++) { // Duyệt cột trong hàng i
            System.out.print(matrix[i][j] + " ");
        }
        System.out.println(); // Xuống dòng sau mỗi hàng
    }
    ```
* **Lưu ý hiệu năng:** Độ phức tạp tăng nhanh (vd: O(N²), O(N³)), cẩn thận khi dữ liệu lớn.

**7. So sánh & Lựa chọn Vòng lặp**

| Đặc điểm                  | `for`                               | `while`                                  | `do-while`                           | `for-each` (`Iterable`/Array)         |
| :------------------------ | :---------------------------------- | :--------------------------------------- | :----------------------------------- | :------------------------------------ |
| **Khi nào dùng**          | Biết số lần lặp, cần index/biến đếm | Số lần lặp không rõ, phụ thuộc điều kiện | Cần chạy ít nhất 1 lần (menu, input) | Duyệt tuần tự tất cả phần tử đơn giản |
| **Kiểm tra điều kiện**    | Trước                               | Trước                                    | Sau                                  | (Ẩn bên trong)                        |
| **Chạy ít nhất 1 lần?**   | Có thể không                        | Có thể không                             | Luôn luôn                            | Có thể không (nếu nguồn rỗng)         |
| **Truy cập index?**       | Có (nếu dùng)                       | Không trực tiếp (cần biến đếm riêng)     | Không trực tiếp (cần biến đếm riêng) | Không                                 |
| **Dễ đọc nhất cho duyệt** | Khá tốt                             | Tùy ngữ cảnh                             | Tùy ngữ cảnh                         | **Thường là tốt nhất**                |

**8. Lỗi Phổ Biến & Thực Tiễn Tốt**

* **Tránh vòng lặp vô hạn:** Đảm bảo điều kiện dừng cuối cùng sẽ `false`, cập nhật biến điều khiển đúng cách.
* **Phạm vi biến:** Khai báo biến trong phạm vi hẹp nhất có thể (thường là trong `for`).
* **Tối ưu hóa:** Tránh tính toán lặp lại không cần thiết trong vòng lặp (đặc biệt là vòng lặp trong cùng). Chỉ tối ưu khi cần thiết.
* **Dễ đọc:** Dùng tên biến ý nghĩa, giữ khối lệnh ngắn gọn (tách hàm nếu phức tạp), thụt lề nhất quán.
* **Ưu tiên `for-each`:** Nếu chỉ cần duyệt qua các phần tử mà không cần index/sửa đổi cấu trúc.
* **Cẩn thận sửa đổi Collection:** Tránh sửa đổi (thêm/xóa) collection khi đang duyệt bằng `for-each` hoặc `for` với index (có thể gây lỗi). Dùng `Iterator` hoặc tạo collection mới nếu cần.