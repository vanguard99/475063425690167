# Cheatsheet: Kế thừa trong Java

## 1. Khai báo Kế thừa

* **Mục đích:** Cho phép lớp con (`SubClass`) thừa hưởng thành viên (không `private`) từ lớp cha (`SuperClass`).
* **Từ khóa:** `extends`
* **Cú pháp:**
    ```java
    class SubClass extends SuperClass {
        // Thân lớp con
    }
    ```
* **Ví dụ:**
    ```java
    class Animal {
        void eat() { /* ... */ }
    }

    class Dog extends Animal { // Dog kế thừa từ Animal
        void bark() { /* ... */ }
    }
    ```

## 2. Từ khóa `super`

* **Mục đích:** Tham chiếu đến thành viên của lớp cha từ lớp con.
* **Sử dụng:**
    * `super()` hoặc `super(args)`: Gọi constructor của lớp cha (phải là dòng đầu tiên trong constructor con).
    * `super.methodName()`: Gọi phương thức bị ghi đè của lớp cha.
    * `super.fieldName`: Truy cập thuộc tính của lớp cha (hữu ích khi có che giấu biến - shadowing).
* **Ví dụ:**
    ```java
    class Parent {
        String name;
        Parent(String name) { this.name = name; }
        void printInfo() { System.out.println("Parent: " + name); }
    }

    class Child extends Parent {
        Child(String name) {
            super(name); // Gọi constructor cha
        }

        @Override
        void printInfo() {
            super.printInfo(); // Gọi phương thức cha
            System.out.println("Child specific info");
        }
    }
    ```

## 3. Ghi đè Phương thức (Method Overriding)

* **Mục đích:** Cung cấp triển khai riêng cho phương thức kế thừa từ lớp cha.
* **Annotation:** `@Override` (Rất khuyến khích sử dụng)
* **Quy tắc chính:**
    * Tên, danh sách tham số (signature) phải giống hệt.
    * Access modifier không được yếu hơn (VD: `protected` -> `public`).
    * Kiểu trả về phải giống hệt hoặc là kiểu con (covariant return type).
    * Không thể ghi đè phương thức `final` hoặc `static`.
* **Ví dụ:**
    ```java
    class Shape {
        void draw() { System.out.println("Drawing shape"); }
    }

    class Circle extends Shape {
        @Override
        void draw() { System.out.println("Drawing circle"); }
    }
    ```

## 4. Lớp `Object`

* **Vai trò:** Lớp gốc (root) của tất cả các lớp trong Java (`java.lang.Object`). Mọi lớp đều ngầm định kế thừa từ `Object`.
* **Các phương thức quan trọng thường được ghi đè:**

| Phương thức          | Mô tả mặc định (của `Object`)                   | Mục đích ghi đè                                                     |
| :------------------- | :---------------------------------------------- | :------------------------------------------------------------------ |
| `toString()`         | `ClassName@hashCode`                            | Trả về chuỗi mô tả đối tượng dễ đọc, hữu ích.                       |
| `equals(Object obj)` | So sánh địa chỉ bộ nhớ (`==`)                   | So sánh trạng thái/nội dung của hai đối tượng.                      |
| `hashCode()`         | Trả về mã hash dựa trên địa chỉ (thường là vậy) | Trả về mã hash dựa trên trạng thái (phải nhất quán với `equals()`). |

* **Ví dụ ghi đè `toString()`:**
    ```java
    class Point {
        int x, y;
        // ... constructor ...
        @Override
        public String toString() {
            return "Point[x=" + x + ", y=" + y + "]";
        }
    }
    ```

## 5. Tính Đa hình (Polymorphism)

* **Khái niệm:** Một biến tham chiếu kiểu lớp cha có thể trỏ đến đối tượng của lớp con.
* **Lợi ích:** Viết mã tổng quát, xử lý nhiều kiểu đối tượng con qua giao diện lớp cha.
* **Liên kết Động (Dynamic Binding):** JVM quyết định gọi phương thức nào (cha hay con) tại *runtime* dựa trên *kiểu thực tế* của đối tượng.
* **Ví dụ:**
    ```java
    Animal myPet = new Dog(); // Polymorphism: Animal reference holds Dog object
    myPet.eat(); // Calls Dog's eat() if overridden, otherwise Animal's eat()

    // Useful with collections
    List<Animal> zoo = new ArrayList<>();
    zoo.add(new Dog());
    zoo.add(new Cat()); // Cat also extends Animal
    for (Animal a : zoo) {
        a.makeSound(); // Calls Dog's or Cat's specific makeSound()
    }
    ```

## 6. Ép kiểu Đối tượng (Object Casting)

* **Upcasting (Ép kiểu ngầm định):** Từ lớp con lên lớp cha. Luôn an toàn, tự động.
    ```java
    Dog dog = new Dog();
    Animal animal = dog; // Implicit upcasting
    ```
* **Downcasting (Ép kiểu tường minh):** Từ lớp cha xuống lớp con. Cần ép kiểu tường minh và có thể gây `ClassCastException`.
    ```java
    Animal animal = new Dog();
    Dog dog = (Dog) animal; // Explicit downcasting - Potentially unsafe
    dog.bark();
    ```
* **Toán tử `instanceof`:** Kiểm tra kiểu thực tế của đối tượng trước khi downcast để tránh `ClassCastException`.
    ```java
    Animal animal = /* could be Dog or Cat */;
    if (animal instanceof Dog) {
        Dog dog = (Dog) animal; // Safe downcast
        dog.bark();
    } else if (animal instanceof Cat) {
        Cat cat = (Cat) animal;
        cat.meow();
    }
    ```
    * *Java 14+ Pattern Matching:*
        ```java
        if (animal instanceof Dog d) { // Check and cast in one step
            d.bark();
        } else if (animal instanceof Cat c) {
            c.meow();
        }
        ```

## 7. Từ khóa `final`

| Sử dụng          | Ý nghĩa trong Kế thừa              | Ví dụ                        |
| :--------------- | :--------------------------------- | :--------------------------- |
| `final class`    | Lớp không thể được kế thừa.        | `final class String { }`     |
| `final method`   | Phương thức không thể bị ghi đè.   | `public final void run()`    |
| `final variable` | Biến chỉ gán giá trị được một lần. | `final int MAX_VALUE = 100;` |

## 8. Điểm Cốt lõi Cần Nhớ

* Kế thừa biểu diễn quan hệ **"IS-A"** (Là một).
* Java chỉ hỗ trợ **Đơn Kế thừa** (Single Inheritance) cho lớp (class). (Sử dụng `interface` để đạt được "đa kế thừa kiểu").
* Thành viên `private` của lớp cha **không** được kế thừa trực tiếp.
* `constructor` **không** được kế thừa, nhưng constructor lớp con **phải** gọi constructor lớp cha (dùng `super()`).
* Ưu tiên **Composition** (quan hệ "HAS-A") hơn Inheritance khi có thể để tăng tính linh hoạt và giảm kopplung.