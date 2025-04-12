##  1. Stack và Heap là gì?

###  **Stack (Ngăn xếp)**

- Là vùng nhớ **nhỏ và nhanh**.
- Dùng để lưu:
  - **biến cục bộ** (local variables)
  - **tham số truyền vào** hàm (method parameters)
  - các **lời gọi hàm** (method calls)
- Mỗi khi bạn gọi một phương thức, Java tạo **một khối trong stack** chứa thông tin về lời gọi đó.
- Khi phương thức kết thúc, **block đó bị loại bỏ**, gọi là *pop khỏi stack*.

> **Đặc điểm chính**: ngăn nắp, ngắn hạn, tốc độ nhanh, tự động thu hồi (vì mỗi khi hàm chạy xong thì phần stack đó sẽ bị xóa đi luôn).

---

###  **Heap (Đống)**

- Là vùng nhớ **lớn hơn**, nhưng **truy xuất chậm hơn**.
- Dùng để lưu:
  - **Đối tượng** (objects)
  - **Biến được tạo bằng `new`**
- Đối tượng nằm trong heap **sống lâu hơn**, và **chỉ bị xóa khi không còn ai dùng** (được dọn bởi Garbage Collector – “Người thu gom rác” của Java).

> **Đặc điểm chính**: rộng rãi, bền vững hơn, quản lý phức tạp, dùng cho đối tượng.

---

##  2. Ẩn dụ: “Quán Phở Java – Bếp & Kho”

Hãy tưởng tượng chương trình Java là một **quán phở**.

###  **Stack là cái… bếp của đầu bếp**

- Nơi đầu bếp làm việc gọn gàng, nhanh gọn lẹ.
- Khi có đơn gọi món, đầu bếp bắt tay vào làm — đặt nguyên liệu lên bếp (biến cục bộ).
- Nấu xong thì… **dẹp bếp** — tức là xóa các biến local đi.

###  **Heap là cái… kho chứa nguyên liệu của quán**

- Khi bạn cần **đặt mua thêm nguyên liệu (new Object)**, bạn bảo nhân viên xuống kho lấy.
- Đã lấy từ kho là phải dùng cẩn thận. Khi không dùng nữa thì **người dọn kho (Garbage Collector)** sẽ tự động dọn giúp.

---

##  3. Ví dụ minh họa

```java
public class Demo {
    public static void main(String[] args) {
        int x = 10;                      // biến primitive -> nằm trên Stack
        String name = "Java";           // chuỗi đặc biệt, nằm ở String Pool (cũng thuộc heap)
        Student s1 = new Student();     // đối tượng -> nằm trên Heap
    }
}
```

- `x`: biến nguyên thủy (primitive) → nằm trên **Stack**.
- `name`: là chuỗi literal, nằm trong **String Pool** (một phần đặc biệt của Heap).
- `s1`: biến tham chiếu nằm trong **Stack**, nhưng đối tượng `Student` thật sự nằm trên **Heap**.

---

##  4. So sánh nhanh Stack vs Heap

| Tiêu chí         | Stack                    | Heap                         |
| ---------------- | ------------------------ | ---------------------------- |
| Dùng để lưu      | Biến local, lời gọi hàm  | Đối tượng, instance          |
| Bộ nhớ           | Nhỏ, nhanh               | Lớn, chậm hơn                |
| Thu hồi bộ nhớ   | Tự động khi hàm kết thúc | Do Garbage Collector quản lý |
| Thời gian sống   | Ngắn hạn                 | Dài hơn, phụ thuộc GC        |
| Tốc độ truy xuất | Rất nhanh                | Chậm hơn một chút            |

---

##  Tổng kết nhẹ

> **Stack** là nơi các hoạt động **tạm thời, nhanh, theo ngăn nắp** diễn ra – như đầu bếp đang nấu ăn.  
> **Heap** là nơi để các **đối tượng sống lâu** hơn trú ngụ – như kho nguyên liệu của quán.
