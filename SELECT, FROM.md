# Lệnh SELECT trong SQL

## 1. Lệnh `SELECT ... FROM ...`
Câu lệnh `SELECT` được dùng để chọn dữ liệu từ cơ sở dữ liệu.

### Cấu trúc:
```sql
SELECT column1, column2, ...
FROM table_name;
```
Lưu ý: `SELECT *` là lấy tất cả dữ liệu trong bảng.

### Ví dụ:
Ta có bảng `Products` với các thông tin như `ProductID`, `ProductName`, ... Nếu muốn lấy tên sản phẩm từ bảng trên thì ta sẽ dùng lệnh `SELECT ... FROM ...` như sau:
```sql
SELECT ProductName
FROM Products;
```
Nếu muốn lấy đơn giá (`UnitPrice`) từ bảng `Products`:
```sql
SELECT UnitPrice
FROM Products;
```
Nếu muốn lấy cả tên sản phẩm lẫn đơn giá:
```sql
SELECT ProductName, UnitPrice
FROM Products;
```

## 2. Lệnh `SELECT DISTINCT ... FROM ...`
Lệnh `SELECT DISTINCT` được sử dụng để lấy ra các giá trị riêng biệt, không trùng lặp.

### Ví dụ:
Ví dụ trong bảng `Customers` có dữ liệu quốc gia (`Country`). Nếu muốn lọc ra những quốc gia khác nhau, ta dùng lệnh sau:
```sql
SELECT DISTINCT Country
FROM Customers;
```
Nếu muốn lấy ra các mã số bưu điện (`PostalCode`) khác nhau từ bảng `Suppliers`:
```sql
SELECT DISTINCT PostalCode
FROM Suppliers;
```

## 3. Câu lệnh `SELECT TOP ... FROM ...`
Lệnh `SELECT TOP` giúp giới hạn số lượng dòng hoặc phần trăm kết quả được trả về.

### Ví dụ:
Lấy ra 10 dòng đầu tiên trong bảng `Customers`:
```sql
SELECT TOP 10 *
FROM Customers;
```
Lấy ra 20% thông tin của nhân viên trong bảng `Employees`:
```sql
SELECT TOP 20 PERCENT *
FROM Employees;
```

## 4. Sử dụng `AS` để đặt Alias (Bí danh)
Alias giúp đổi tên cột hoặc bảng để dễ đọc hơn.

### Ví dụ:
Đặt bí danh cho cột `ProductName` và `UnitPrice`:
```sql
SELECT ProductName AS 'Tên Sản Phẩm', UnitPrice AS 'Giá'
FROM Products;
```
Đặt bí danh cho bảng `Customers`:
```sql
SELECT C.CustomerName, C.City
FROM Customers AS C;
```

## 5. Sử dụng các hàm tính toán
SQL cung cấp các hàm tính toán như `SUM`, `AVG`, `MIN`, `MAX`.

### Ví dụ:
Tính tổng giá trị sản phẩm:
```sql
SELECT SUM(UnitPrice) AS TotalPrice
FROM Products;
```
Tính giá trung bình:
```sql
SELECT AVG(UnitPrice) AS AvgPrice
FROM Products;
```

## 6. Sử dụng `COUNT` để đếm số lượng bản ghi
Hàm `COUNT` dùng để đếm số lượng hàng trong bảng.

### Ví dụ:
Đếm số lượng khách hàng:
```sql
SELECT COUNT(*) AS TotalCustomers
FROM Customers;
```
Đếm số sản phẩm có giá lớn hơn 100:
```sql
SELECT COUNT(*) AS ExpensiveProducts
FROM Products
WHERE UnitPrice > 100;
```

## Kết luận
Các lệnh `SELECT`, `DISTINCT`, `TOP`, alias, hàm tính toán và `COUNT` giúp chúng ta truy vấn dữ liệu hiệu quả trong SQL. Tiếp tục khám phá các câu lệnh nâng cao để tối ưu truy vấn dữ liệu!

---
### NỘI DUNG: Lê Đức Mạnh
---
#### [BÀI TIẾP THEO: WHERE](https://github.com/DABTMU/SQLwithDAB/blob/main/WHERE.md)
