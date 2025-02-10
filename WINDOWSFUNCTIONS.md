# Windows Functions trong SQL

## 1. Giới thiệu về Windows Functions 🌟🌟🌟
Windows Functions trong SQL được sử dụng để thực hiện các phép tính trên một nhóm các hàng có liên quan đến dòng hiện tại. Khác với Aggregate Functions tính toán trên toàn bộ tập dữ liệu và trả về một giá trị duy nhất, Windows Functions vẫn giữ nguyên từng hàng của dữ liệu gốc và chỉ thêm cột tính toán dựa trên một cửa sổ (window) xác định.

Một Windows Function được định nghĩa khi có mệnh đề `OVER()` đi kèm sau lệnh gọi hàm.

## 2. Cú pháp của Windows Functions 📝🔄🌐
```sql
Windows_Function () OVER (
    [PARTITION BY partition_expression, ...]
    [ORDER BY sort_expression [ASC | DESC], ...]
)
```
### Các thành phần:
- **`PARTITION BY`**: Dùng để nhóm các hàng có liên quan thành một partition để thực hiện việc tính toán.
- **`ORDER BY`**: Dùng để sắp xếp các hàng trong từng partition đó.

Khi sử dụng Windows Functions, các kết quả trả về được tính toán trong từng partition mà không làm thay đổi số lượng hàng của dữ liệu gốc.

## 3. Các loại Windows Functions 🌐🔢📊
Windows Functions trong SQL được chia thành ba nhóm chính:

### 3.1. Aggregate Functions
| Tên hàm | Miêu tả |
|---------|---------|
| `AVG()` | Trả về giá trị trung bình |
| `COUNT()` | Đếm số lượng giá trị |
| `MAX()` | Trả về giá trị lớn nhất |
| `MIN()` | Trả về giá trị nhỏ nhất |
| `SUM()` | Tính tổng các giá trị |

### 3.2. Ranking Functions
| Tên hàm | Miêu tả |
|---------|---------|
| `RANK()` | Xếp hạng các giá trị theo thứ tự tăng dần, giá trị trùng nhau có cùng hạng, nhưng thứ hạng tiếp theo sẽ bị bỏ qua (Ví dụ: `1,1,3,4,5`). |
| `DENSE_RANK()` | Giống `RANK()`, nhưng không bỏ qua thứ hạng tiếp theo (Ví dụ: `1,1,2,3,4`). |
| `ROW_NUMBER()` | Gán số thứ tự duy nhất cho mỗi hàng trong từng partition theo thứ tự tăng dần. |
| `CUME_DIST()` | Tính tỷ lệ các giá trị nhỏ hơn hoặc bằng giá trị hiện tại. |
| `PERCENT_RANK()` | Tính toán theo công thức `(rank - 1) / (row - 1)`. |

### 3.3. Analytic Functions
| Tên hàm | Miêu tả |
|---------|---------|
| `FIRST_VALUE(expression)` | Lấy giá trị đầu tiên trong mỗi partition. |
| `LAST_VALUE(expression)` | Lấy giá trị cuối cùng trong mỗi partition. |
| `LAG(expression, offset)` | Lấy giá trị của hàng trước đó theo thứ tự sắp xếp. `offset` là số hàng bỏ qua, mặc định là `1`. |
| `LEAD(expression, offset)` | Lấy giá trị của hàng sau đó theo thứ tự sắp xếp. `offset` là số hàng bỏ qua, mặc định là `1`. |

## 4. Ví dụ sử dụng Windows Functions 🎨📊📚
### Ví dụ 1: Xếp hạng khách hàng theo tổng doanh thu hàng tháng
Giả sử có bảng `Sales` với dữ liệu sau:

| CustomerID | Month | Revenue |
|------------|-------|---------|
| 1          | 1     | 1000    |
| 2          | 1     | 1500    |
| 3          | 1     | 2000    |
| 1          | 2     | 1800    |
| 2          | 2     | 2200    |
| 3          | 2     | 2500    |

Sử dụng `RANK()` để xếp hạng khách hàng theo doanh thu từng tháng:
```sql
SELECT CustomerID, Month, Revenue,
       RANK() OVER (PARTITION BY Month ORDER BY Revenue DESC) AS Rank
FROM Sales;
```

### Ví dụ 2: So sánh doanh thu tháng hiện tại với tháng trước
Sử dụng `LAG()` để lấy doanh thu tháng trước của từng khách hàng:
```sql
SELECT CustomerID, Month, Revenue,
       LAG(Revenue, 1) OVER (PARTITION BY CustomerID ORDER BY Month) AS PrevMonthRevenue
FROM Sales;
```

## 5. Ứng dụng của Windows Functions trong SQL 🔄👥🌟
Windows Functions thường được sử dụng để:
- **Tính toán trong từng nhóm dữ liệu**, ví dụ như xếp hạng khách hàng theo từng tháng.
- **Tạo số thứ tự cho từng hàng** mà không cần sử dụng các phương pháp phức tạp.
- **So sánh dữ liệu theo dòng thời gian**, chẳng hạn như so sánh doanh thu tháng hiện tại với tháng trước.
- **Phân tích xu hướng và mẫu dữ liệu**, chẳng hạn như tìm giá trị đầu tiên hoặc cuối cùng của một tập dữ liệu.

Windows Functions là một công cụ mạnh mẽ trong SQL giúp đơn giản hóa việc tính toán và phân tích dữ liệu trong từng nhóm mà không làm thay đổi cấu trúc của tập dữ liệu gốc.

---
### NỘI DUNG: Bùi Trịnh Minh Ngọc
---
### Bài tiếp theo
