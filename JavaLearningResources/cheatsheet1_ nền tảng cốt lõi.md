**Cheatsheet Java Nền Tảng Cốt Lõi**

**1. Cấu trúc Cơ bản & Khởi chạy**

* **Khai báo Lớp (Class):** Mọi code Java nằm trong lớp. Tên file `.java` phải trùng tên lớp `public`.
    ```java
    public class TenLop {
        // Nội dung lớp ở đây
    }
    ```
* **Phương thức `main` (Điểm khởi đầu):**
    ```java
    public static void main(String[] args) {
        // Chương trình bắt đầu từ đây
        System.out.println("Bắt đầu!");
    }
    ```
    * `public`: Truy cập từ mọi nơi.
    * `static`: Gọi không cần tạo đối tượng.
    * `void`: Không trả về giá trị.
    * `main`: Tên chuẩn JVM tìm kiếm.
    * `String[] args`: Mảng chứa tham số dòng lệnh.
* **In ra Console:**
    ```java
    System.out.println("Nội dung cần in và xuống dòng");
    System.out.print("In nội dung không xuống dòng");
    ```
* **Ghi chú (Comments):**
    ```java
    // Ghi chú một dòng
    /* Ghi chú
       nhiều dòng */
    /** Javadoc comment để tạo tài liệu */
    ```
* **Câu lệnh (Statement):** Kết thúc bằng dấu chấm phẩy `;`.
* **Khối mã (Code Block):** Định nghĩa bởi cặp dấu ngoặc nhọn `{ }`.

**2. Công cụ JDK Chính (CLI)**

* `javac TenFile.java`: Biên dịch mã nguồn `.java` thành bytecode `.class`.
* `java TenLop`: Khởi chạy JVM để thực thi bytecode từ lớp `TenLop` (lớp chứa phương thức `main`).
* `jar`: Đóng gói tệp `.class` và tài nguyên thành tệp `.jar`.
* `javadoc`: Tạo tài liệu API từ Javadoc comments.

**3. Biến và Hằng số**

* **Khai báo biến:** `dataType variableName;`
    * Quy tắc đặt tên: `camelCase` (ví dụ: `soLuong`, `tenSinhVien`). Không bắt đầu bằng số, không chứa ký tự đặc biệt (trừ `_`, `$`), không trùng từ khóa.
    ```java
    int tuoi; // Khai báo
    tuoi = 30; // Gán giá trị
    double diemTrungBinh = 8.5; // Khai báo và khởi tạo
    String hoTen = "Nguyễn Văn A";
    boolean daKichHoat = true;
    char kyTu = 'X';
    ```
* **Khai báo hằng số:** Dùng `final`. Giá trị không đổi sau khi gán lần đầu.
    * Quy tắc đặt tên: `UPPER_SNAKE_CASE` (ví dụ: `SO_PI`, `MAX_USERS`).
    ```java
    final double PI = 3.14159;
    final int THOI_GIAN_CHO_TOI_DA = 1000; // milliseconds
    final String LOI_CHAO_MAC_DINH = "Xin chào!";
    ```

**4. Kiểu Dữ liệu (Data Types)**

* **Nguyên thủy (Primitive Types):** Lưu trữ giá trị trực tiếp.

| Kiểu      | Kích thước | Mô tả                | Khoảng giá trị           | Giá trị mặc định* |
| :-------- | :--------- | :------------------- | :----------------------- | :---------------- |
| `byte`    | 1 byte     | Số nguyên có dấu     | -128 đến 127             | `0`               |
| `short`   | 2 bytes    | Số nguyên có dấu     | -32,768 đến 32,767       | `0`               |
| `int`     | 4 bytes    | Số nguyên có dấu     | -2³¹ đến 2³¹-1           | `0`               |
| `long`    | 8 bytes    | Số nguyên có dấu lớn | -2⁶³ đến 2⁶³-1           | `0L`              |
| `float`   | 4 bytes    | Số thực đơn          | ~±3.4e±38 (thêm `F`/`f`) | `0.0f`            |
| `double`  | 8 bytes    | Số thực kép          | ~±1.7e±308               | `0.0d`            |
| `boolean` | ~1 bit     | Logic (đúng/sai)     | `true` hoặc `false`      | `false`           |
| `char`    | 2 bytes    | Ký tự Unicode        | `\u0000` đến `\uffff`    | `\u0000`          |

\* *Giá trị mặc định chỉ áp dụng cho biến instance/static, không áp dụng cho biến cục bộ (local).* Biến cục bộ phải được khởi tạo trước khi dùng.

* **Tham chiếu (Reference Types):** Lưu trữ địa chỉ bộ nhớ của đối tượng.
    * Các lớp (Built-in: `String`, `Integer`,... Custom: `TenLop`,...)
    * Mảng (`int[]`, `String[][]`,...)
    * Interfaces, Enums.
    * Giá trị mặc định (cho biến instance/static): `null`. `null` nghĩa là không trỏ đến đối tượng nào.

**5. Ép kiểu (Type Casting)**

* **Ngầm định (Widening):** Từ nhỏ sang lớn (an toàn).
    `byte` -> `short` -> `int` -> `long` -> `float` -> `double`
    ```java
    int soNguyen = 100;
    long soLon = soNguyen; // Tự động
    double soThuc = soLon; // Tự động
    ```
* **Tường minh (Narrowing):** Từ lớn sang nhỏ (có thể mất dữ liệu). Cú pháp: `(targetType) value`
    ```java
    double diem = 9.78;
    int diemNguyen = (int) diem; // Bắt buộc ép kiểu, kết quả: 9
    long giaTriLon = 12345678901L;
    int giaTriNho = (int) giaTriLon; // Có thể bị tràn số nếu giaTriLon quá lớn
    ```

**6. Toán tử (Operators)**

* **Số học:** `+`, `-`, `*`, `/` (chia nguyên nếu cả hai toán hạng là nguyên), `%` (chia lấy dư).
    ```java
    int a = 10 / 3; // a = 3
    double b = 10.0 / 3; // b = 3.333...
    int du = 10 % 3; // du = 1
    ```
* **Gán:** `=`, `+=`, `-=`, `*=`, `/=`, `%=`
    ```java
    int x = 5;
    x += 3; // Tương đương x = x + 3; (x giờ là 8)
    ```
* **Một ngôi:** `+` (dấu dương), `-` (dấu âm), `++` (tăng 1), `--` (giảm 1), `!` (phủ định logic NOT).
    * `++var` (Prefix): Tăng trước, trả về giá trị mới.
    * `var++` (Postfix): Trả về giá trị cũ, tăng sau.
    * `--` tương tự.
    ```java
    int count = 5;
    int pre = ++count; // count=6, pre=6
    int post = count++; // post=6, count=7
    boolean ok = true;
    boolean notOk = !ok; // notOk = false
    ```
* **So sánh:** `==` (bằng), `!=` (không bằng), `>`, `<`, `>=`, `<=` (Trả về `boolean`).
    ***Lưu ý:*** Dùng `==` để so sánh giá trị kiểu nguyên thủy. Dùng `.equals()` để so sánh nội dung của đối tượng (như `String`).
    ```java
    String s1 = "Test";
    String s2 = new String("Test");
    boolean compareRef = (s1 == s2); // false (so sánh địa chỉ)
    boolean compareContent = s1.equals(s2); // true (so sánh nội dung)
    ```
* **Logic:** `&&` (AND - short-circuit), `||` (OR - short-circuit), `!` (NOT).
    * Short-circuit: Vế sau không được đánh giá nếu kết quả đã rõ từ vế trước.
    ```java
    boolean dieuKien = (tuoi > 18) && (diem >= 5.0);
    ```
* **Điều kiện (Ternary):** `condition ? value_if_true : value_if_false`
    ```java
    String ketQua = (diem >= 5.0) ? "Đạt" : "Trượt";
    ```
* **Độ ưu tiên (Precedence - cơ bản):** `()` > `++ -- !` (một ngôi) > `* / %` > `+ -` (số học) > `> < >= <= == !=` (so sánh) > `&&` > `||` > `=` (gán). Dùng `()` để làm rõ hoặc thay đổi thứ tự.

**7. Cấu trúc Điều khiển Luồng**

* **`if`:** Thực thi nếu điều kiện đúng.
    ```java
    if (dieuKienBoolean) {
        // Lệnh khi đúng
    }
    ```
* **`if-else`:** Thực thi một trong hai khối.
    ```java
    if (dieuKienBoolean) {
        // Lệnh khi đúng
    } else {
        // Lệnh khi sai
    }
    ```
* **`if-else if-else`:** Kiểm tra nhiều điều kiện tuần tự.
    ```java
    if (dieuKien1) {
        // Lệnh 1
    } else if (dieuKien2) {
        // Lệnh 2
    } else {
        // Lệnh mặc định (nếu không có cái nào đúng)
    }
    ```
* **`switch-case`:** So sánh một biến với nhiều hằng số. Dùng cho `byte`, `short`, `char`, `int`, `String` (từ Java 7), `Enum`.
    ```java
    switch (bienHoacBieuThuc) {
        case GIA_TRI_1:
            // Lệnh cho giá trị 1
            break; // QUAN TRỌNG: Thoát khỏi switch
        case GIA_TRI_2:
            // Lệnh cho giá trị 2
            break;
        // ... các case khác
        default: // Tùy chọn: Nếu không khớp case nào
            // Lệnh mặc định
            break; // Thường không cần ở default nhưng có thể đặt
    }
    ```
    ***Lưu ý "Fall-through":*** Nếu thiếu `break`, code sẽ chạy tiếp sang `case` tiếp theo. Dùng có chủ đích khi muốn gộp case:
    ```java
    case 9:
    case 10:
    case 11:
        // Cùng xử lý cho 9, 10, 11
        break;
    ```

**8. Best Practices & Lỗi Phổ Biến**

* **Đặt tên:** `PascalCase` cho Lớp/Interface, `camelCase` cho Biến/Phương thức, `UPPER_SNAKE_CASE` cho Hằng số (`final static`). Dùng tên có ý nghĩa.
* **Định dạng:** Thụt lề nhất quán (thường 4 spaces), dùng dấu cách quanh toán tử, dùng công cụ format tự động (Ctrl+Alt+L trong IntelliJ).
* **Ghi chú:** Giải thích phần phức tạp, tránh ghi chú thừa. Dùng `/** Javadoc */` cho API.
* **Tránh "Magic Numbers":** Dùng hằng số `final` thay vì giá trị số trực tiếp không rõ nghĩa.
* **Lỗi thường gặp:**
    * Nhầm `=` (gán) với `==` (so sánh).
    * So sánh `String` bằng `==` thay vì `.equals()`.
    * Quên `break` trong `switch`.
    * Chia số nguyên (`5 / 2` ra `2`).
    * Quên `;` hoặc lỗi cặp `{}`.
    * Dùng biến cục bộ chưa khởi tạo.
    * `NullPointerException` (NPE): Gọi phương thức/truy cập thuộc tính trên biến `null`. Luôn kiểm tra `!= null` trước khi dùng.
    * Lỗi chính xác `float`/`double` cho tính toán tài chính (dùng `BigDecimal`).