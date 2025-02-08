# 📌 Mệnh đề WHERE trong SQL

## 🔹 1. Giới thiệu
- Mệnh đề `WHERE` được sử dụng để **lọc các bản ghi**.
- Dùng để **trích xuất những bản ghi đáp ứng một điều kiện cụ thể**.

### 🔹 Cấu trúc:
```sql
SELECT column1, column2, ...
FROM Table_name 
WHERE condition1, condition2, ...;
```

## 🔹 2. Ví dụ cơ bản
📍 **Lấy ra thông tin của các nhân viên đến từ LONDON**:
```sql
SELECT * 
FROM Employees 
WHERE [City] = 'London';
```

---

## 🔹 3. Các loại toán tử thường dùng trong WHERE

### 🔸 3.1. Toán tử so sánh ⚖️
Dùng để so sánh giá trị trong cột với một giá trị cụ thể. Một số toán tử phổ biến:

| Toán tử | Ý nghĩa |
|---------|--------|
| =       | Bằng |
| <> hoặc != | Khác |
| >       | Lớn hơn |
| <       | Nhỏ hơn |
| >=      | Lớn hơn hoặc bằng |
| <=      | Nhỏ hơn hoặc bằng |

📍 **Ví dụ**: Lấy sản phẩm có giá lớn hơn **50$**:
```sql
SELECT * 
FROM Products 
WHERE UnitPrice > 50;
```

---

### 🔸 3.2. Toán tử AND, OR, NOT 🧩
#### 🔹 Toán tử `AND`
✔ Kết hợp nhiều điều kiện, chỉ trả về bản ghi **thoả mãn tất cả các điều kiện**.

📍 **Ví dụ**: Lấy nhân viên sống ở **Hà Nội** và **có tuổi lớn hơn 30**:
```sql
SELECT * 
FROM Employees 
WHERE [City] = 'Ha Noi' AND Age > 30;
```

#### 🔹 Toán tử `OR`
✔ Kết hợp điều kiện, chỉ cần **một điều kiện đúng** thì bản ghi sẽ được chọn.

📍 **Ví dụ**: Lấy sản phẩm có giá **lớn hơn 60$ hoặc nhỏ hơn 30$**:
```sql
SELECT * 
FROM Products 
WHERE UnitPrice > 60 OR UnitPrice < 30;
```

#### 🔹 Toán tử `NOT`
✔ Dùng để phủ định một điều kiện nào đó.

📍 **Ví dụ**: Lấy nhân viên **không sống ở New York**:
```sql
SELECT * 
FROM Employees 
WHERE NOT [City] = 'New York';
```

---

### 🔸 3.3. Toán tử `BETWEEN` 📏
✔ Dùng để chọn các giá trị trong một phạm vi nhất định (bao gồm cả hai đầu).

📍 **Cấu trúc:**
```sql
SELECT column_name(s) 
FROM table_name 
WHERE column_name BETWEEN value1 AND value2;
```

📍 **Ví dụ**: Lấy sản phẩm có giá từ **10$ đến 20$**:
```sql
SELECT * 
FROM Products 
WHERE UnitPrice BETWEEN 10 AND 20;
```

---

### 🔸 3.4. Toán tử `LIKE` 🔍
✔ Dùng để tìm kiếm chuỗi có dạng cụ thể.
✔ Ký tự đại diện thường dùng:
  - `%` : Đại diện cho **0, 1 hoặc nhiều ký tự**.
  - `_` : Đại diện cho **1 ký tự đơn**.

📍 **Ví dụ 1**: Lấy sản phẩm **bắt đầu bằng chữ 'A'**:
```sql
SELECT ProductName, UnitPrice 
FROM Products 
WHERE ProductName LIKE 'A%';
```

📍 **Ví dụ 2**: Lấy tên công ty **kết thúc bằng chữ 'c' và trước đó chỉ có 1 ký tự**:
```sql
SELECT CompanyName 
FROM Suppliers 
WHERE CompanyName LIKE '_c';
```

---

### 🔸 3.5. Toán tử `IN` 🎯
✔ Tương tự như `OR` nhưng dùng để kiểm tra nhiều giá trị cùng lúc.

📍 **Cấu trúc:**
```sql
SELECT column_name(s) 
FROM table_name 
WHERE column_name IN (value1, value2, ...);
```

📍 **Ví dụ**: Lấy đơn hàng được vận chuyển về **Brazil hoặc Việt Nam**:
```sql
SELECT * 
FROM Orders 
WHERE ShipCountry IN ('Brazil', 'Viet Nam');
```

---

### 🔸 3.6. Toán tử `IS NULL` và `IS NOT NULL` ❓
✔ Dùng để kiểm tra giá trị `NULL`.

📍 **Ví dụ 1**: Lấy khách hàng **chưa có số điện thoại**:
```sql
SELECT * 
FROM Customers 
WHERE PhoneNumber IS NULL;
```

📍 **Ví dụ 2**: Lấy nhân viên **đã có số điện thoại**:
```sql
SELECT * 
FROM Employees 
WHERE PhoneNumber IS NOT NULL;
```

---
### NỘI DUNG: Lê Đức Mạnh
