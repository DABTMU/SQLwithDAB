# 7. GROUP BY và HAVING trong SQL

## I. Tổng quan

Trong SQL, `GROUP BY` và `HAVING` là hai câu lệnh rất quan trọng khi làm việc với dữ liệu tổng hợp. Chúng thường được sử dụng cùng với các hàm **aggregate** như: `COUNT()`, `SUM()`, `AVG()`, `MIN()`, `MAX()` để nhóm dữ liệu và lọc ra những nhóm có điều kiện nhất định.

---

## II. Câu lệnh GROUP BY

### ✅ Mục đích:

* **`GROUP BY`** được dùng để **nhóm các dòng dữ liệu có cùng giá trị trong một hoặc nhiều cột**.
* Thường đi kèm với các hàm tổng hợp (aggregate functions).

### ✅ Cú pháp:

```sql
SELECT column1, aggregate_function(column2)
FROM table_name
GROUP BY column1;
```

---

### 📌 Ví dụ:

Cho bảng `Orders`:

| OrderID | CustomerID | Amount |
| ------- | ---------- | ------ |
| 1       | A          | 100    |
| 2       | B          | 200    |
| 3       | A          | 150    |
| 4       | C          | 300    |
| 5       | B          | 250    |

### ➤ Câu truy vấn:

```sql
SELECT CustomerID, SUM(Amount) AS TotalAmount
FROM Orders
GROUP BY CustomerID;
```

### 🔍 Kết quả:

| CustomerID | TotalAmount |
| ---------- | ----------- |
| A          | 250         |
| B          | 450         |
| C          | 300         |

**Giải thích:** Dữ liệu được nhóm theo `CustomerID`, sau đó tổng `Amount` được tính cho từng nhóm.

---

## III. Câu lệnh HAVING

### ✅ Mục đích:

* **`HAVING`** được dùng để **lọc các nhóm** sau khi đã được nhóm bởi `GROUP BY`.
* Khác với `WHERE` (lọc từng dòng trước khi nhóm), `HAVING` dùng **để lọc các nhóm sau khi đã tổng hợp**.

### ✅ Cú pháp:

```sql
SELECT column1, aggregate_function(column2)
FROM table_name
GROUP BY column1
HAVING aggregate_function(column2) condition;
```

---

### 📌 Ví dụ tiếp theo:

```sql
SELECT CustomerID, SUM(Amount) AS TotalAmount
FROM Orders
GROUP BY CustomerID
HAVING SUM(Amount) > 300;
```

### 🔍 Kết quả:

| CustomerID | TotalAmount |
| ---------- | ----------- |
| B          | 450         |
| C          | 300         |

**Giải thích:** Nhóm của Customer A có tổng `Amount = 250` nên bị loại bỏ. Chỉ những nhóm có tổng lớn hơn hoặc bằng 300 mới được giữ lại.

---

## IV. So sánh WHERE và HAVING

| Tiêu chí          | WHERE                | HAVING             |
| ----------------- | -------------------- | ------------------ |
| Thời điểm lọc     | Trước khi `GROUP BY` | Sau khi `GROUP BY` |
| Dùng với          | Các dòng (rows)      | Các nhóm (groups)  |
| Dùng với hàm tổng | ❌ Không              | ✅ Có thể           |

---

## V. Ví dụ kết hợp WHERE - GROUP BY - HAVING

```sql
SELECT CustomerID, COUNT(*) AS OrderCount
FROM Orders
WHERE Amount > 100
GROUP BY CustomerID
HAVING COUNT(*) >= 2;
```

**Giải thích:**

1. `WHERE Amount > 100`: chỉ lấy các dòng có `Amount > 100`.
2. `GROUP BY CustomerID`: nhóm theo `CustomerID`.
3. `HAVING COUNT(*) >= 2`: chỉ giữ lại nhóm có ít nhất 2 đơn hàng sau khi lọc.

---

## VI. Kết luận

* Sử dụng `GROUP BY` để **gom nhóm dữ liệu** dựa trên giá trị của một hoặc nhiều cột.
* Dùng `HAVING` để **lọc các nhóm đã được tổng hợp**, nhất là khi kết hợp với hàm tổng hợp.
* Kết hợp nhuần nhuyễn `WHERE`, `GROUP BY` và `HAVING` giúp bạn phân tích dữ liệu linh hoạt và sâu sắc hơn trong SQL.

---

## VII. Thực hành đề xuất

Bạn có thể thực hành các truy vấn sau trên một hệ cơ sở dữ liệu như MySQL, PostgreSQL hoặc SQLite:

```sql
-- Tổng số đơn hàng mỗi khách hàng đã đặt
SELECT CustomerID, COUNT(OrderID) AS TotalOrders
FROM Orders
GROUP BY CustomerID;

-- Chỉ lấy các khách hàng có tổng số đơn hàng >= 3
SELECT CustomerID, COUNT(OrderID) AS TotalOrders
FROM Orders
GROUP BY CustomerID
HAVING COUNT(OrderID) >= 3;
```

---

*🧠 Tip nhỏ: Khi nghi ngờ giữa WHERE và HAVING – nhớ rằng `WHERE` là lọc trước khi nhóm, còn `HAVING` là lọc sau khi nhóm!*
