# **Tối ưu hóa truy vấn SQL trong SQL Server**  

Tối ưu hóa SQL giúp tăng tốc độ xử lý truy vấn, giảm tải hệ thống, và cải thiện hiệu suất tổng thể của cơ sở dữ liệu SQL Server.

---
## ⚠️ Nội dung này đang được cập nhật và chỉnh sửa
---

## **1. Sử dụng Execution Plan và SQL Server Profiler**
- **Execution Plan**: Dùng `Actual Execution Plan` hoặc `Estimated Execution Plan` trong SSMS để phân tích truy vấn.
- **SQL Server Profiler**: Theo dõi truy vấn chậm và tài nguyên sử dụng.
- **Kiểm tra hiệu suất truy vấn**:
  ```sql
  SET STATISTICS IO ON;
  SET STATISTICS TIME ON;
  SELECT * FROM orders WHERE customer_id = 1001;
  ```

---

## **2. Tối ưu hóa Indexing**
### **2.1. Các loại Index**
- **Clustered Index**: Tự động được tạo trên `PRIMARY KEY`, giúp tăng tốc độ truy vấn.
- **Non-Clustered Index**: Dùng cho các cột thường xuyên được lọc trong `WHERE` hoặc `JOIN`.
- **Filtered Index**: Dùng khi chỉ có một số hàng thường xuyên được truy vấn.

### **2.2. Tạo Index hiệu quả**
```sql
CREATE NONCLUSTERED INDEX idx_orders_customer 
ON orders(customer_id) 
INCLUDE (order_date, total_price);
```

### **2.3. Kiểm tra Index bị thiếu**
```sql
SELECT * FROM sys.dm_db_missing_index_details;
```

---

## **3. Cập nhật thống kê (`UPDATE STATISTICS`)**
Cập nhật thống kê giúp Query Optimizer hoạt động chính xác hơn.
```sql
UPDATE STATISTICS orders;
```

---

## **4. Tránh `SELECT *`, sử dụng `WITH (NOLOCK)` nếu chỉ đọc dữ liệu**
```sql
SELECT order_id, customer_id FROM orders WITH (NOLOCK);
```
⚠️ **Lưu ý:** `WITH (NOLOCK)` có thể trả về dữ liệu chưa commit.

---

## **5. Partitioning trong SQL Server**
Dùng `PARTITION BY` để chia bảng thành nhiều phần nhỏ.
```sql
CREATE PARTITION FUNCTION pfOrderRange (DATETIME)
AS RANGE LEFT FOR VALUES ('2024-01-01', '2024-07-01');

CREATE PARTITION SCHEME psOrderScheme
AS PARTITION pfOrderRange ALL TO ([PRIMARY]);
```

---

## **6. Sử dụng `TABLE VARIABLE` thay vì `TEMP TABLE` khi dữ liệu nhỏ**
📌 **Table Variable (Nhanh hơn với dữ liệu nhỏ, không tạo thống kê)**
```sql
DECLARE @TempOrders TABLE (order_id INT, customer_id INT);
INSERT INTO @TempOrders SELECT order_id, customer_id FROM orders WHERE order_date > '2024-01-01';
```

📌 **Temp Table (Tốt hơn với dữ liệu lớn, có thể tạo Index)**
```sql
CREATE TABLE #TempOrders (order_id INT, customer_id INT);
INSERT INTO #TempOrders SELECT order_id, customer_id FROM orders WHERE order_date > '2024-01-01';
CREATE INDEX idx_temp_orders ON #TempOrders (customer_id);
```

---

## **7. Sử dụng Stored Procedures để tối ưu xử lý**
```sql
CREATE PROCEDURE GetOrdersByCustomer @customerId INT
AS
BEGIN
    SET NOCOUNT ON;
    SELECT * FROM orders WHERE customer_id = @customerId;
END;
```
```sql
EXEC GetOrdersByCustomer @customerId = 1001;
```

---

## **8. Tránh sử dụng `CURSOR`, thay bằng `SET BASED QUERY`**
❌ **Dùng CURSOR (Chậm và tốn tài nguyên)**
```sql
DECLARE order_cursor CURSOR FOR
SELECT order_id FROM orders;
OPEN order_cursor;
FETCH NEXT FROM order_cursor INTO @order_id;
```
✅ **Dùng Set-Based Query (Nhanh hơn)**
```sql
UPDATE orders SET status = 'Processed' WHERE order_date < '2024-01-01';
```

---

## **9. Giới hạn số lượng bản ghi trả về**
```sql
SELECT * FROM orders ORDER BY order_date DESC OFFSET 0 ROWS FETCH NEXT 100 ROWS ONLY;
```

---

## **10. Kiểm tra và tối ưu hóa Deadlocks**
### **10.1. Kiểm tra Deadlocks**
```sql
SELECT * FROM sys.dm_tran_locks;
```
### **10.2. Giảm Deadlocks bằng cách luôn cập nhật theo cùng thứ tự**
```sql
BEGIN TRANSACTION;
UPDATE customers SET balance = balance - 100 WHERE customer_id = 1;
UPDATE accounts SET balance = balance + 100 WHERE account_id = 2;
COMMIT TRANSACTION;
```

---

## **Kết luận**
| Kỹ thuật | Hiệu quả |
|----------|---------|
| **Indexing** | Giảm thời gian quét bảng |
| **Cập nhật thống kê** | Cải thiện tốc độ Query Optimizer |
| **Tối ưu JOIN** | Tránh quét toàn bộ dữ liệu |
| **Dùng Partitioning** | Chia nhỏ dữ liệu, tăng hiệu suất |
| **Stored Procedures** | Giúp xử lý nhanh hơn |
| **Tránh CURSOR** | Hạn chế tiêu tốn tài nguyên |
| **Dùng Table Variable / Temp Table hợp lý** | Giảm tải hệ thống |
| **Tối ưu Deadlocks** | Tránh xung đột giao dịch |

---
### NỘI DUNG: Bùi Trịnh Minh Ngọc

