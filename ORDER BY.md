# 🔃 SQL ORDER BY - Sắp xếp dữ liệu như dân chuyên

## 💡 ORDER BY là gì?

`ORDER BY` là câu lệnh dùng để **sắp xếp** các bản ghi trong kết quả truy vấn SQL theo một hoặc nhiều cột, theo thứ tự **tăng dần (ASC)** hoặc **giảm dần (DESC)**.

### 🔗 Cú pháp chuẩn:

```sql
SELECT column1, column2
FROM table_name
ORDER BY column1 [ASC|DESC], column2 [ASC|DESC];
```

---

## 🧩 Các kiểu sắp xếp phổ biến

### 🔸 1. Sắp xếp theo một cột

```sql
SELECT * FROM Products
ORDER BY price ASC;
```

📌 Sắp xếp sản phẩm theo giá tăng dần.

### 🔸 2. Sắp xếp giảm dần

```sql
SELECT name, salary FROM Employees
ORDER BY salary DESC;
```

📌 Xem danh sách nhân viên lương cao nhất đến thấp nhất.

### 🔸 3. Sắp xếp nhiều cột

```sql
SELECT name, department, salary FROM Employees
ORDER BY department ASC, salary DESC;
```

📌 Trong mỗi phòng ban, sắp xếp nhân viên theo lương cao xuống thấp.

---

## 🧠 ORDER BY với các kiểu dữ liệu khác nhau

### 🧮 Sắp xếp số:

```sql
SELECT product_name, quantity FROM Inventory
ORDER BY quantity ASC;
```

### 🔤 Sắp xếp chữ:

```sql
SELECT name FROM Students
ORDER BY name ASC;
```

### 📅 Sắp xếp ngày tháng:

```sql
SELECT name, join_date FROM Members
ORDER BY join_date DESC;
```

---

## 💼 Các ví dụ thực tế thường gặp

### 🛍️ 1. Danh sách sản phẩm giá rẻ nhất:

```sql
SELECT name, price FROM Products
ORDER BY price ASC
LIMIT 10;
```

### 🧾 2. Hóa đơn mới nhất:

```sql
SELECT * FROM Invoices
ORDER BY created_at DESC;
```

### 👨‍💼 3. Top nhân viên doanh thu cao:

```sql
SELECT name, total_sales FROM Employees
ORDER BY total_sales DESC
LIMIT 5;
```

### 🗃️ 4. Danh sách khách hàng theo tên và ngày đăng ký:

```sql
SELECT name, signup_date FROM Customers
ORDER BY name ASC, signup_date DESC;
```

---

## 💎 ORDER BY nâng cao

### 🎯 Sắp xếp với biểu thức tính toán:

```sql
SELECT name, unit_price, quantity, unit_price * quantity AS total
FROM Orders
ORDER BY total DESC;
```

📌 Tính tổng tiền từng đơn và sắp xếp theo giá trị lớn nhất.

### 🧪 Dùng CASE WHEN để sắp xếp tùy biến:

```sql
SELECT name, status FROM Tasks
ORDER BY
  CASE
    WHEN status = 'urgent' THEN 1
    WHEN status = 'normal' THEN 2
    WHEN status = 'low' THEN 3
    ELSE 4
  END;
```

📌 Sắp xếp công việc theo độ ưu tiên do ta định nghĩa.

---

## 🚀 Tối ưu hóa khi dùng ORDER BY

* Dùng `LIMIT` để giới hạn số bản ghi khi sắp xếp với dữ liệu lớn.
* Đảm bảo có **chỉ mục (index)** trên cột cần sắp xếp để tăng tốc độ.
* Tránh sắp xếp trên kết quả `DISTINCT`, `GROUP BY` hoặc `JOIN` phức tạp nếu không cần thiết.

---

## ✅ Tổng kết

| Tính năng            | Mục đích                                                            |
| -------------------- | ------------------------------------------------------------------- |
| ORDER BY column ASC  | Sắp xếp tăng dần (mặc định)                                         |
| ORDER BY column DESC | Sắp xếp giảm dần                                                    |
| ORDER BY nhiều cột   | Sắp xếp theo nhiều tiêu chí                                         |
| ORDER BY + LIMIT     | Lấy top kết quả sau khi sắp xếp                                     |
| ORDER BY biểu thức   | Sắp xếp theo tính toán động (giá trị tổng, trạng thái tuỳ chỉnh...) |

👉 ORDER BY không chỉ đơn giản là sắp xếp — đó là nghệ thuật trình bày dữ liệu đúng cách, đúng lúc!

---

🧪 Gợi ý luyện tập:

1. Viết truy vấn để sắp xếp sinh viên theo điểm GPA giảm dần.
2. Lấy top 3 sản phẩm bán chạy nhất theo doanh thu.
3. Sắp xếp bài viết blog theo độ ưu tiên custom (VIP > Premium > Free).

---

✨ SQL giỏi không chỉ SELECT, mà còn phải biết sắp xếp đúng người – đúng lúc – đúng dữ liệu 😎
