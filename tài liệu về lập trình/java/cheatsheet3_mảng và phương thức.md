## Cheatsheet: Mảng (Arrays) và Phương thức (Methods) trong Java

### Mảng (Arrays)

#### 1. Khai báo

```java
// Cách 1 (Ưa chuộng)
kiểu_dữ_liệu[] tên_biến_mảng;
// Ví dụ:
int[] scores;
String[] names;

// Cách 2 (Giống C/C++)
kiểu_dữ_liệu tên_biến_mảng[];
// Ví dụ:
double studentGrades[];
```

* Biến mảng chỉ là **tham chiếu**, ban đầu có giá trị `null`.

#### 2. Khởi tạo

* **Dùng `new` (cần kích thước):**
    ```java
    tên_biến_mảng = new kiểu_dữ_liệu[kích_thước];
    // Ví dụ:
    scores = new int[5]; // Mảng int 5 phần tử
    names = new String[10]; // Mảng String 10 phần tử

    // Kết hợp khai báo và khởi tạo:
    int[] dataPoints = new int[100];
    ```
* **Khởi tạo nhanh (Array Initializer - tự xác định kích thước):**
    ```java
    kiểu_dữ_liệu[] tên_biến_mảng = {giá_trị_0, giá_trị_1, ...};
    // Ví dụ:
    double[] coefficients = {1.9, 2.9, 3.4, 3.5};
    String[] weekdays = {"Thứ Hai", "Thứ Ba", ...};
    boolean[] flags = {true, false, true};
    ```
* **Giá trị mặc định khi dùng `new`:**
    * Số (`byte`, `short`, `int`, `long`, `float`, `double`): `0` hoặc `0.0`
    * `char`: `\u0000` (ký tự null)
    * `boolean`: `false`
    * Tham chiếu (Đối tượng, `String`): `null`

#### 3. Truy cập và Thao tác

* **Truy cập phần tử:** Dùng chỉ số (index) từ `0` đến `length - 1`.
    ```java
    int[] myNumbers = {10, 20, 30};
    int first = myNumbers[0]; // first = 10
    int last = myNumbers[myNumbers.length - 1]; // last = 30
    ```
* **Gán giá trị:**
    ```java
    String[] fruits = new String[3];
    fruits[0] = "Apple";
    fruits[1] = "Mango"; // Thay đổi giá trị
    ```
* **Lấy độ dài (kích thước):** Thuộc tính `length` (không phải phương thức).
    ```java
    int size = scores.length; // Lấy số phần tử của mảng scores
    ```
* **Lỗi `ArrayIndexOutOfBoundsException`:** Xảy ra khi truy cập chỉ số ngoài phạm vi `[0, length - 1]`.

#### 4. Duyệt Mảng

* **Vòng lặp `for` truyền thống (cần chỉ số hoặc thay đổi mảng):**
    ```java
    int[] values = {5, 10, 15};
    for (int i = 0; i < values.length; i++) {
        System.out.println("Index " + i + ": " + values[i]);
        // values[i] = values[i] * 2; // Có thể thay đổi
    }
    ```
* **Vòng lặp `for-each` (chỉ cần đọc giá trị, gọn hơn):**
    ```java
    String[] languages = {"Java", "Python"};
    for (String lang : languages) {
        System.out.println("Language: " + lang);
        // lang = "C++"; // Không thay đổi mảng gốc
    }
    ```

#### 5. Mảng Đa chiều (Ví dụ: 2 chiều - Ma trận)

* **Khai báo & Khởi tạo (Chữ nhật):**
    ```java
    kiểu_dữ_liệu[][] tên_mảng;
    tên_mảng = new kiểu_dữ_liệu[số_hàng][số_cột];
    // Ví dụ:
    int[][] matrix = new int[3][4]; // 3 hàng, 4 cột
    ```
* **Khởi tạo nhanh:**
    ```java
    int[][] table = {
        {1, 2, 3},
        {4, 5, 6}
    }; // Mảng 2x3
    ```
* **Truy cập:** `tên_mảng[chỉ_số_hàng][chỉ_số_cột]`
    ```java
    matrix[0][0] = 10;
    int value = table[1][2]; // value = 6
    ```
* **Mảng Răng cưa (Jagged Array - các hàng khác độ dài):**
    ```java
    int[][] jaggedArray = new int[3][]; // Khởi tạo số hàng
    jaggedArray[0] = new int[2]; // Hàng 0 có 2 cột
    jaggedArray[1] = new int[4]; // Hàng 1 có 4 cột
    jaggedArray[0][1] = 5;
    ```
* **Duyệt (Vòng lặp lồng nhau):**
    ```java
    // Dùng for truyền thống
    for (int row = 0; row < table.length; row++) { // table.length là số hàng
        for (int col = 0; col < table[row].length; col++) { // table[row].length là số cột của hàng row
            System.out.print(table[row][col] + "\t");
        }
        System.out.println();
    }

    // Dùng for-each
    for (int[] row : table) {
        for (int element : row) {
            System.out.print(element + "\t");
        }
        System.out.println();
    }
    ```

#### 6. Lớp `java.util.Arrays` (Cần `import java.util.Arrays;`)

| Phương thức Static         | Mô tả cực ngắn                                                      | Ví dụ sử dụng                                        |
| :------------------------- | :------------------------------------------------------------------ | :--------------------------------------------------- |
| `sort(array)`              | Sắp xếp mảng tăng dần.                                              | `Arrays.sort(numbers);`                              |
| `binarySearch(array, key)` | Tìm `key` trong mảng **đã sắp xếp**. Trả về chỉ số hoặc giá trị âm. | `int index = Arrays.binarySearch(sortedNumbers, 5);` |
| `equals(array1, array2)`   | So sánh nội dung hai mảng có bằng nhau không.                       | `boolean isEqual = Arrays.equals(arr1, arr2);`       |
| `fill(array, value)`       | Gán `value` cho tất cả phần tử mảng.                                | `Arrays.fill(counts, 0);`                            |
| `copyOf(original, newLen)` | Tạo bản sao mảng với độ dài `newLen`.                               | `int[] copy = Arrays.copyOf(original, 10);`          |
| `copyOfRange(orig, f, t)`  | Tạo bản sao từ chỉ số `f` (bao gồm) đến `t` (không bao gồm).        | `int[] part = Arrays.copyOfRange(original, 2, 5);`   |
| `toString(array)`          | Trả về biểu diễn chuỗi của mảng (hữu ích khi debug).                | `System.out.println(Arrays.toString(numbers));`      |

#### 7. So sánh `Array` và `ArrayList<E>`

| Đặc điểm           | Mảng (`Array`)                                      | `ArrayList<E>` (từ `java.util`)                       |
| :----------------- | :-------------------------------------------------- | :---------------------------------------------------- |
| **Kích thước**     | Cố định (Fixed size) sau khi khởi tạo.              | Động (Dynamic size), có thể thêm/xóa phần tử.         |
| **Kiểu dữ liệu**   | Nguyên thủy (`int`, `double`...) & Đối tượng.       | Chỉ Đối tượng (Dùng Wrapper: `Integer`, `Double`...). |
| **Khai báo**       | `type[] name;` hoặc `type name[];`                  | `ArrayList<Type> name = new ArrayList<>();`           |
| **Thêm phần tử**   | Không có phương thức trực tiếp (phải tạo mảng mới). | `add(element)`, `add(index, element)`                 |
| **Xóa phần tử**    | Không có phương thức trực tiếp.                     | `remove(index)`, `remove(object)`                     |
| **Lấy kích thước** | Thuộc tính `length`                                 | Phương thức `size()`                                  |
| **Truy cập**       | `array[index]` (Nhanh, O(1))                        | `get(index)` (Nhanh, thường O(1))                     |
| **Thay đổi**       | `array[index] = value;`                             | `set(index, value)`                                   |
| **Hiệu năng**      | Nhanh hơn cho truy cập trực tiếp.                   | Chậm hơn chút, đặc biệt khi thay đổi kích thước.      |
| **API**            | Cơ bản (`java.util.Arrays`)                         | Phong phú (Collections Framework)                     |

* **Chọn Mảng khi:** Biết chắc kích thước cố định, cần hiệu năng tối ưu, lưu kiểu nguyên thủy trực tiếp.
* **Chọn ArrayList khi:** Kích thước thay đổi, cần thêm/xóa thường xuyên, muốn dùng tiện ích Collections.

---

### Phương thức (Methods)

#### 1. Định nghĩa (Syntax)

```java
modifiers returnType methodName(parameterList) throws ExceptionList {
    // Method body (thân phương thức)
    // Câu lệnh thực thi
    // [return value;] // Nếu returnType không phải void
}
```

* `modifiers`: (Tùy chọn)
    * Quyền truy cập: `public`, `private`, `protected`, (mặc định - package-private)
    * Khác: `static` (thuộc về lớp, gọi bằng `TênLớp.methodName()`), `final` (không bị override), `abstract` (không có body, trong abstract class/interface), `synchronized` (đa luồng).
* `returnType`: Kiểu dữ liệu trả về. Dùng `void` nếu không trả về gì.
* `methodName`: Tên phương thức (quy tắc camelCase, ví dụ: `calculateSum`).
* `parameterList`: (Tùy chọn) Danh sách tham số trong `()`, cách nhau bởi dấu phẩy (`kiểu_dữ_liệu tên_tham_số`). Để trống `()` nếu không có tham số.
* `throws ExceptionList`: (Tùy chọn) Khai báo các checked exceptions có thể ném ra.
* `Method body`: Khối lệnh trong `{}`. Phải có `return value;` nếu `returnType` khác `void`.

* **Chữ ký phương thức (Method Signature):** `methodName` + `parameterList` (kiểu dữ liệu và thứ tự). Dùng để phân biệt trong nạp chồng. Kiểu trả về **KHÔNG** thuộc chữ ký.

#### 2. Gọi Phương thức (Invocation)

* **Phương thức `static`:**
    * `TênLớp.tênPhươngThức(đối_số);`
    * `tênPhươngThức(đối_số);` (Nếu gọi từ trong cùng lớp)
* **Phương thức non-static (của đối tượng):**
    ```java
    // 1. Tạo đối tượng
    TênLớp tênĐốiTượng = new TênLớp();
    // 2. Gọi phương thức qua đối tượng
    tênĐốiTượng.tênPhươngThức(đối_số);
    ```
* **Đối số (Arguments):** Giá trị thực tế truyền vào khi gọi, phải khớp với tham số (số lượng, kiểu, thứ tự).
* **Xử lý giá trị trả về (nếu không `void`):** Gán vào biến, dùng trong biểu thức, in ra, hoặc bỏ qua.

#### 3. Truyền Tham số (Parameter Passing) - **Luôn là Truyền Giá Trị (Pass-by-Value)**

* **Kiểu Nguyên thủy (`int`, `float`, `boolean`...):** Truyền **bản sao của giá trị**. Thay đổi tham số bên trong phương thức **không** ảnh hưởng biến gốc bên ngoài.
* **Kiểu Tham chiếu (Đối tượng, Mảng):** Truyền **bản sao của giá trị tham chiếu (địa chỉ)**.
    * Cả tham số (bên trong) và biến gốc (bên ngoài) cùng trỏ đến **cùng một đối tượng** trên Heap.
    * **Thay đổi trạng thái/nội dung** của đối tượng qua tham số bên trong (vd: `arrParam[0] = 99;`, `objParam.setAttribute(newValue);`) **SẼ ảnh hưởng** đến đối tượng gốc.
    * **Gán tham chiếu mới** cho tham số bên trong (vd: `arrParam = new int[10];`, `objParam = null;`) **KHÔNG ảnh hưởng** đến tham chiếu gốc bên ngoài (biến gốc vẫn trỏ đến đối tượng ban đầu).

#### 4. Nạp chồng Phương thức (Method Overloading)

* Định nghĩa nhiều phương thức **cùng tên** trong cùng một lớp.
* **Điều kiện:** Danh sách tham số phải khác nhau về:
    * Số lượng tham số, HOẶC
    * Kiểu dữ liệu tham số, HOẶC
    * Thứ tự kiểu dữ liệu tham số.
* **Lưu ý:** Kiểu trả về (`returnType`) hoặc `modifiers` **KHÔNG** dùng để phân biệt nạp chồng.
* **Lợi ích:** Tăng tính linh hoạt và dễ đọc của API (vd: `System.out.println()` nạp chồng cho nhiều kiểu).

#### 5. Phạm vi Biến (Variable Scope)

* **Biến cục bộ (Local Variables):**
    * Khai báo bên trong phương thức/khối lệnh `{}`.
    * Chỉ truy cập được trong khối lệnh chứa nó, từ điểm khai báo trở đi.
    * **Phải khởi tạo** trước khi dùng.
    * Tồn tại trên Stack, bị hủy khi ra khỏi khối lệnh.
    * Tham số phương thức cũng là biến cục bộ.
* **Biến instance (Instance Variables / Fields):**
    * Khai báo trong lớp, ngoài phương thức.
    * Mỗi đối tượng có bản sao riêng.
    * Truy cập từ phương thức non-static cùng lớp.
    * Có giá trị mặc định.
    * Tồn tại trên Heap cùng đối tượng.
* **Biến lớp (Class Variables / `static` Variables):**
    * Khai báo như biến instance + `static`.
    * Chỉ có **một bản sao duy nhất** cho cả lớp.
    * Truy cập từ phương thức static/non-static (thường dùng `TênLớp.tênBiếnStatic`).
    * Có giá trị mặc định.
    * Tồn tại suốt chương trình.

#### 6. Đệ quy (Recursion)

* Phương thức tự gọi lại chính nó.
* **Cần có:**
    1.  **Trường hợp cơ sở (Base Case):** Điều kiện dừng, trả về giá trị cụ thể, không gọi đệ quy nữa. **BẮT BUỘC** để tránh lặp vô hạn.
    2.  **Bước đệ quy (Recursive Step):** Gọi lại chính nó với đầu vào thay đổi (thường nhỏ hơn/gần base case), kết hợp kết quả.
* **Ví dụ (Giai thừa):**
    ```java
    public static long factorial(int n) {
        if (n < 0) throw new IllegalArgumentException("Số âm không có giai thừa");
        // Base case
        if (n == 0 || n == 1) {
            return 1;
        }
        // Recursive step
        else {
            return n * factorial(n - 1);
        }
    }
    ```
* **Ưu điểm:** Mã ngắn gọn, thanh lịch cho một số bài toán (cây, chia để trị).
* **Nhược điểm:** Tốn bộ nhớ stack, chậm hơn vòng lặp, nguy cơ `StackOverflowError` nếu đệ quy quá sâu hoặc thiếu base case.

#### 7. Phương thức `main`

```java
public static void main(String[] args) {
    // Điểm bắt đầu của ứng dụng Java độc lập
    // args: Mảng String chứa các đối số dòng lệnh (command-line arguments)
}
```

* `public`: JVM có thể gọi từ bên ngoài.
* `static`: JVM gọi không cần tạo đối tượng của lớp chứa `main`.
* `void`: Không trả về giá trị cho JVM.
* `main`: Tên quy ước JVM tìm kiếm.
* `String[] args`: Tham số bắt buộc, nhận đối số dòng lệnh.