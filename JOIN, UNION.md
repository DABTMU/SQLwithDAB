# 🧠 SQL JOIN & UNION - Kiến Thức Chi Tiết

## 🔹 5. JOIN - Kết hợp nhiều bảng dữ liệu

### 💡 JOIN là gì?

JOIN trong SQL được sử dụng để kết hợp các bản ghi từ hai hay nhiều bảng lại với nhau dựa trên mối quan hệ giữa các cột.

### 🔗 Các loại JOIN phổ biến:

#### 🔸 INNER JOIN

Chỉ lấy những bản ghi có giá trị khớp nhau ở cả hai bảng.

```sql
SELECT Employees.name, Departments.department_name
FROM Employees
INNER JOIN Departments
ON Employees.department_id = Departments.id;
```

🧪 **Ví dụ thực tế:**

* Lấy danh sách nhân viên cùng tên phòng ban họ đang làm việc.

#### 🔸 LEFT JOIN (hoặc LEFT OUTER JOIN)

Lấy tất cả bản ghi từ bảng bên trái, và các bản ghi khớp từ bảng bên phải. Nếu không khớp thì trả về NULL.

```sql
SELECT Customers.name, Orders.order_date
FROM Customers
LEFT JOIN Orders
ON Customers.id = Orders.customer_id;
```

🧪 **Ví dụ thực tế:**

* Tìm tất cả khách hàng, kể cả khách chưa từng đặt hàng.

#### 🔸 RIGHT JOIN (hoặc RIGHT OUTER JOIN)

Tương tự LEFT JOIN nhưng ưu tiên bảng bên phải.

```sql
SELECT Employees.name, Salaries.salary
FROM Employees
RIGHT JOIN Salaries
ON Employees.id = Salaries.employee_id;
```

🧪 **Ví dụ thực tế:**

* Tìm thông tin lương cho tất cả người có bảng lương, kể cả khi không có nhân viên tương ứng.

#### 🔸 FULL OUTER JOIN

Lấy tất cả bản ghi từ cả hai bảng, khớp thì nối, không khớp thì trả về NULL.

```sql
SELECT A.id, A.name, B.salary
FROM Employees A
FULL OUTER JOIN Salaries B
ON A.id = B.employee_id;
```

🧪 **Ví dụ thực tế:**

* Tạo danh sách tổng hợp nhân viên và bảng lương dù có khớp hay không.

#### 🔸 SELF JOIN

JOIN chính bảng đó với chính nó.

```sql
SELECT A.name AS Employee, B.name AS Manager
FROM Employees A
JOIN Employees B ON A.manager_id = B.id;
```

🧪 **Ví dụ thực tế:**

* Xác định người quản lý của mỗi nhân viên trong cùng bảng `Employees`.

#### 🔸 CROSS JOIN

Tạo tích Descartes giữa hai bảng.

```sql
SELECT A.name, B.product
FROM Customers A
CROSS JOIN Products B;
```

🧪 **Ví dụ thực tế:**

* Tạo danh sách tất cả các tổ hợp khách hàng - sản phẩm (sử dụng cho chiến dịch marketing).

---

## 🔹 6. UNION - Hợp nhất kết quả nhiều truy vấn

### 💡 UNION là gì?

Dùng để kết hợp kết quả từ hai hoặc nhiều câu lệnh `SELECT`. Mặc định sẽ loại bỏ các bản ghi trùng lặp.

### 🔗 Cú pháp:

```sql
SELECT column1, column2 FROM table1
UNION
SELECT column1, column2 FROM table2;
```

### 🧩 Các loại UNION:

#### 🔸 UNION

Loại bỏ bản ghi trùng lặp giữa các tập hợp kết quả.

```sql
SELECT city FROM Customers_US
UNION
SELECT city FROM Customers_EU;
```

🧪 **Ví dụ thực tế:**

* Tạo danh sách duy nhất các thành phố có khách hàng ở Mỹ và Châu Âu.

#### 🔸 UNION ALL

Giữ lại tất cả các bản ghi, kể cả trùng lặp.

```sql
SELECT product_name FROM Sales_2023
UNION ALL
SELECT product_name FROM Sales_2024;
```

🧪 **Ví dụ thực tế:**

* Gộp doanh số bán hàng của hai năm để làm thống kê chi tiết.

### 🛑 Lưu ý khi dùng UNION:

* Số lượng cột trong các `SELECT` phải bằng nhau.
* Thứ tự và kiểu dữ liệu các cột tương ứng cũng phải giống nhau.
* `ORDER BY` chỉ có thể áp dụng ở cuối cùng của toàn bộ UNION.

### 💼 Thực tiễn ứng dụng:

1. **Gộp dữ liệu lịch sử:**

```sql
SELECT name, created_at FROM Users_2023
UNION ALL
SELECT name, created_at FROM Users_2024;
```

2. **Tạo báo cáo tổng hợp đa bảng:**

```sql
SELECT id, name, 'Customer' AS Type FROM Customers
UNION
SELECT id, name, 'Supplier' AS Type FROM Suppliers;
```

3. **Tìm kiếm đa vùng dữ liệu:**

```sql
SELECT name FROM North_Region_Employees
UNION
SELECT name FROM South_Region_Employees;
```

---

## ✅ Tổng kết

| JOIN/UNION | Dùng để làm gì?                                           |
| ---------- | --------------------------------------------------------- |
| JOIN       | Kết hợp dữ liệu theo mối quan hệ giữa các bảng            |
| UNION      | Gộp kết quả của nhiều truy vấn `SELECT`                   |
| INNER JOIN | Chỉ kết hợp các bản ghi khớp nhau                         |
| LEFT JOIN  | Lấy tất cả từ bảng trái, khớp thì nối, không khớp là NULL |
| RIGHT JOIN | Ngược lại với LEFT JOIN                                   |
| FULL JOIN  | Lấy tất cả bản ghi từ cả hai bảng                         |
| CROSS JOIN | Tạo tổ hợp tất cả các bản ghi                             |
| UNION ALL  | Giữ cả bản ghi trùng lặp khi gộp                          |

Muốn vững JOIN và UNION thì luyện tập là chìa khóa vàng 🗝️ — Let’s SQL like a boss 😎📈!
