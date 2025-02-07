# Tổng quan về các câu lệnh SELECT trong SQL

## 1. Lệnh SELECT...FROM...

- Câu lệnh **SELECT** được dùng để chọn dữ liệu từ cơ sở dữ liệu.  
  **Cấu trúc:**
  ```sql
  SELECT column1, column2, ...
  ```
  **Lưu ý:** `SELECT *` là lấy tất cả dữ liệu trong bảng.
  
- Câu lệnh **FROM**:
  - Là nơi chứa dữ liệu để lệnh `SELECT` lấy dữ liệu.
  - Điền tên bảng mà ta muốn lấy dữ liệu.
  
  **Cấu trúc:**
  ```sql
  FROM table_name
  ```

### Ví dụ:
Giả sử ta có bảng `Products` với các thông tin như `ProductID`, `ProductName`,...
- Lấy tên sản phẩm:
  ```sql
  SELECT ProductName
  FROM Products;
  ```
- Lấy đơn giá (`UnitPrice`):
  ```sql
  SELECT UnitPrice
  FROM Products;
  ```
- Lấy cả tên sản phẩm lẫn đơn giá:
  ```sql
  SELECT ProductName, UnitPrice
  FROM Products;
  ```

## 2. Lệnh SELECT DISTINCT...FROM...

- Về cơ bản, lệnh này giống với `SELECT...FROM...`, nhưng khác ở chỗ:
  - `SELECT...FROM...` lấy ra dữ liệu có thể bị trùng lặp.
  - `SELECT DISTINCT...FROM...` chỉ lấy ra dữ liệu riêng biệt, không trùng lặp.

### Ví dụ:
- Lọc ra danh sách các quốc gia khác nhau từ bảng `Customers`:
  ```sql
  SELECT DISTINCT Country
  FROM Customers;
  ```
- Lọc các mã số bưu điện khác nhau từ bảng `Suppliers`:
  ```sql
  SELECT DISTINCT PostalCode
  FROM Suppliers;
  ```

## 3. Câu lệnh SELECT TOP...FROM...

- `SELECT TOP...FROM...` giới hạn số lượng dòng (hoặc phần trăm %) kết quả được trả về.

### Ví dụ:
- Lấy ra 10 dòng đầu tiên của bảng `Customers`:
  ```sql
  SELECT TOP 10 *
  FROM Customers;
  ```
- Lấy ra 20% thông tin nhân viên từ bảng `Employees`:
  ```sql
  SELECT TOP 20 PERCENT *
  FROM Employees;
  ```

## 4. Mệnh đề WHERE

- `WHERE` được sử dụng để **lọc** các bản ghi.
- Chỉ trích xuất những bản ghi đáp ứng **điều kiện cụ thể**.

**Cấu trúc:**
```sql
SELECT (DISTINCT, TOP) column1, column2, ...
FROM table_name
WHERE condition1 AND condition2 ...;
```

### Ví dụ:
Giả sử ta có bảng `Employees`, nếu muốn lấy thông tin nhân viên đến từ **London**, ta viết lệnh như sau:
```sql
SELECT *
FROM Employees
WHERE City = 'London';
```
---
### NỘI DUNG: LÊ ĐỨC MẠNH 
