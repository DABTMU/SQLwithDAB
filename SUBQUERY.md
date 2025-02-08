# 📌 TRUY VẤN CON (SUBQUERY)

## 📖 Khái niệm
Truy vấn con (Subquery) thường được dùng trong các câu truy vấn đòi hỏi tính toán phức tạp. Chúng ta sử dụng Subquery khi cần tính toán dữ liệu, tạo ra một bảng dữ liệu tạm thời mới. Truy vấn con được sử dụng một lần trong câu lệnh truy vấn nơi nó xác định. 

Các truy vấn con có thể xuất hiện trong các mệnh đề khác nhau của một truy vấn bên ngoài hoặc trong hoạt động set. Chúng phải được đặt trong ngoặc đơn `()`. Nếu kết quả của truy vấn con được so sánh với một cái gì đó khác, số cột phải khớp. Có thể sử dụng Truy vấn con (Subquery) trong các câu lệnh như `SELECT`, `FROM`, `JOIN` hoặc bất kì phép toán tập hợp nào.

## 🏗 Cấu trúc chung của Subquery
```sql
SELECT column1, column2,...
FROM table1
WHERE column_name OPERATOR ( SELECT column_name FROM table1 WHERE condition);
```

---
## 🔍 1. Subquery in WHERE clause
### 📌 Cú pháp
```sql
SELECT column1, column2,...
FROM table1
WHERE Column_name OPERATOR ( SELECT column_name FROM table2 WHERE condition)
```
📌 **Trong đó:**
- **`OPERATOR`**: có thể là `=`, `>`, `<`, `>=`, `<=`, `IN`, `NOT IN`, `EXISTS`, `NOT EXISTS`.
- **Subquery**: Truy vấn con bên trong dấu ngoặc đơn `()` trả về một hoặc nhiều giá trị để so sánh với cột của bảng chính.

📌 **Ví dụ:**
Truy vấn tất cả khách hàng có thành phố là `'Fresno'` trong bảng `sales.customers`.
```sql
SELECT *
FROM sales.customers
WHERE CITY IN ( SELECT city FROM sales.customers WHERE city = 'Fresno')
```

---
## 🎯 2. Subquery in SELECT clause
Subquery có thể được sử dụng trong `SELECT` để tính toán hoặc lấy dữ liệu bổ sung cho từng dòng của truy vấn chính.
- **Phải trả về duy nhất 1 giá trị**.
- **Thường kết hợp với các hàm tổng hợp** như `COUNT()`, `SUM()`, `AVG()`, `MAX()`, `MIN()`.

### 📌 Cú pháp
```sql
SELECT column1,
       (SELECT column_name FROM table2 WHERE condition) AS alias_name
FROM table1;
```
📌 **Ví dụ:**
Truy vấn các khách hàng đã mua hàng ở cửa hàng `2`.
```sql
SELECT sales.orders.customer_id, 
       (SELECT count(*) FROM sales.orders WHERE sales.orders.store_id = '2') as ph
FROM sales.orders
```

---
## 🏛 3. Subquery in FROM clause
Subquery trong `FROM` giúp tạo một bảng tạm thời để sử dụng trong truy vấn chính.
- Có thể kết hợp với `JOIN`, `GROUP BY`, `HAVING`,... để lấy dữ liệu phức tạp hơn.

### 📌 Cú pháp
```sql
SELECT Col_1, Col_2,...
FROM (SELECT Col_1, Col_2 FROM Table_1 WHERE condition) AS Subquery_Name
```
📌 **Ví dụ:**
Đếm tất cả khách hàng đã đặt hàng vào ngày `'2016-01-27'`.
```sql
SELECT count(*)
FROM (SELECT * FROM sales.orders WHERE sales.orders.order_date = '2016-01-27') as mtp
```

---
## 🔄 4. Truy vấn con tương quan (Correlated Subquery)
Truy vấn con tương quan là một truy vấn con mà mỗi lần thực hiện đều phụ thuộc vào từng dòng của truy vấn chính.

### 📌 Cú pháp
```sql
SELECT Col_1, Col_2,...
FROM Table_1 AS tb1
WHERE Col_Name OPERATOR (
    SELECT Col_3 FROM Table_2 AS tb2
    WHERE tb1.Related_Col = tb2.Related_Col)
```
📌 **Ví dụ:**
Truy vấn các khách hàng đã đặt ít nhất `1` đơn hàng.
```sql
SELECT a.first_name , a.last_name
FROM sales.customers as a 
WHERE a.customer_id in (
       SELECT b.customer_id 
       FROM sales.orders as b 
       WHERE a.customer_id = b.customer_id and b.customer_id is not null)
```

---
## 📂 5. Lọc kết quả truy vấn bằng truy vấn trên bảng khác nhau
Có thể sử dụng `Subquery` hoặc `JOIN` để lọc dữ liệu từ một bảng dựa trên dữ liệu của một bảng khác.

📌 **Ví dụ:**
Lọc `order_id` của khách hàng có thành phố `'Fresno'`.
```sql
SELECT a.order_id 
FROM sales.orders as a 
WHERE a.customer_id in (
    SELECT customer_id FROM sales.customers as b 
    WHERE b.city in (
        SELECT city FROM sales.customers WHERE city = 'Fresno'))
```
---
### NỘI DUNG: Trần Thị Thuý Huyền
