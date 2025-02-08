# 🏗 Bảng chứa dữ liệu tạm thời (Common Table Expressions - CTE)
## 📖 Khái niệm
CTE giúp lưu trữ dữ liệu trong một khoảng thời gian ngắn trong phiên làm việc, giúp xử lý dữ liệu trung gian mà không làm ảnh hưởng đến dữ liệu gốc.

## 📌 Cú pháp
```sql
WITH CTE_Name (Col_1, Col_2,...) AS (
    SELECT Col_1, Col_2
    FROM Table
    WHERE Condition)
SELECT Col_3, Col_4
FROM CTE_Name;
```
📌 **Ví dụ:**
Lập bảng dữ liệu tạm thời với `city` và `phone` cho khách hàng tên `'Theo'`.
```sql
WITH mtp as 
  ( SELECT city , phone 
   FROM sales.customers 
   WHERE sales.customers.first_name = 'Theo' ) 
SELECT * FROM mtp;
```
---
📌 **Ứng dụng của CTE:**
- **Tái sử dụng nhiều lần trong cùng một truy vấn** giúp tối ưu hiệu suất.
- **Dễ đọc và dễ bảo trì hơn so với Subquery lồng nhau**.
- **Có thể sử dụng đệ quy để xử lý dữ liệu cây phân cấp**.

📌 **Ví dụ về CTE đệ quy:**  
*ví dụ không sử dụng database bikestore*  
Truy vấn danh sách nhân viên và cấp trên của họ từ bảng `employees`.
```sql
WITH RecursiveCTE AS (
    SELECT employee_id, manager_id, full_name
    FROM employees
    WHERE manager_id IS NULL
    UNION ALL
    SELECT e.employee_id, e.manager_id, e.full_name
    FROM employees e
    JOIN RecursiveCTE r ON e.manager_id = r.employee_id
)
SELECT * FROM RecursiveCTE;
```
---
### NỘI DUNG: Trần Thị Thuý Huyền
