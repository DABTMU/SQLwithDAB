# 📌 CÁC KIỂU DỮ LIỆU VÀ CÁCH XỬ LÝ TRONG SQL  

## 📖 1. Các kiểu dữ liệu trong SQL  

### 1.1. Dữ liệu dạng số  
- **BIT**: Số nguyên có thể là 0, 1 hoặc NULL
- **TINYINT**: Cho phép các số nguyên từ 0 đến 255 (1 byte)  
- **SMALLINT**: Cho phép các số nguyên từ -32.768 đến 32.767 (2 byte)
- **INT**: Cho phép các số nguyên từ -2.147.483.648 đến 2.147.483.647 (4 byte)
- **BIGINT**: Cho phép các số nguyên trong khoảng -9.223.372.036.854.775.808 đến 9.223.372.036.854.775.807 (8 byte)
- **DECIMAL(p,s)**:	Đã cố định độ chính xác và số tỷ lệ. Cho phép các số từ -1038 +1 đến 1038 -1.  
*Tham số p cho biết tổng số chữ số tối đa có thể được lưu trữ (cả bên trái và bên phải của dấu thập phân). p phải là giá trị từ 1 đến 38. Mặc định là 18.  
 Tham số s cho biết số lượng chữ số tối đa được lưu trữ ở bên phải của dấu thập phân. s phải là một giá trị từ 0 đến p. Giá trị mặc định là 0.*	(5-17 byte)
- **NUMERIC(p,s)**: Đã cố định độ chính xác và số tỷ lệ. Cho phép các số từ -1038 +1 đến 1038 -1.  
*Tham số p cho biết tổng số chữ số tối đa có thể được lưu trữ (cả bên trái và bên phải của dấu thập phân). p phải là giá trị từ 1 đến 38. Mặc định là 18.  
Tham số s cho biết số lượng chữ số tối đa được lưu trữ ở bên phải của dấu thập phân. s phải là một giá trị từ 0 đến p. Giá trị mặc định là 0* (5-17 byte)
- **SMALLMONEY**: Dữ liệu tiền tệ từ -214.748.3648 đến 214.748.3647 (4 byte)
- **MONEY**: Dữ liệu tiền tệ từ -922.337.203.685.477.5808 đến 922.337.203.685.477.5807	8 byte
- **FLOAT(n)**: Dữ liệu số chính xác từ -1,79E + 308 đến 1,79E + 308. Tham số n cho biết trường nên giữ 4 hay 8 byte. float (24) giữ trường 4 byte và float (53) giữ trường 8 byte. Giá trị mặc định của n là 53. (4 hoặc 8 byte)
- **REAL**: Dữ liệu số chính xác từ -3,40E + 38 đến 3,40E + 38	(4 byte)

### 1.2. Dữ liệu dạng ký tự  
#### Dữ liệu dạng chuỗi ký tự
- CHAR[( n | max)]: Lưu trữ chuỗi ký tự có kích thước cố định, tương ứng n.
- VARCHAR [( n | max)]: Dữ liệu chuỗi có kích thước linh hoạt, kích thước tương ứng n hoặc
max.
- TEXT: Lưu trữ các chuỗi ký tự lớn, định dạng TEXT không có tham biến, nhưng sẽ lưu trữ tối
đa trong phạm vi khoảng 2GB, trong khi đó VARCHAR có thể lưu trữ với phạm vi ngắn
khoảng 8000 byte.
#### Dữ liệu dạng chuỗi nhị phân
- BINARY: Dùng để lưu trữ các dãy byte có độ dài cố định.
#### Dữ liệu dạng ký tự Unicode
- N được viết ở đầu mỗi định dạng cho phép lưu trữ ký tự Unicode.
- NCHAR [( n | max)]: Lưu trữ chuỗi có độ dài cố định, có kích thước tương ứng n hoặc max
và cho phép lưu trữ dưới dạng Unicode.
- NVARCHAR [( n | max)]: Lưu trữ chuỗi ký tự có độ dài linh hoạt, có kích thước tương ứng n
hoặc max, cho phép Unicode.
- NTEXT: Chuỗi ký tự có độ dài linh hoạt, tối đa lưu trữ khoảng 1073741823 byte, cho phép
Unicode.


### 1.3. Dữ liệu dạng ngày giờ  
- **DATE, TIME, DATETIME, TIMESTAMP** – Lưu trữ thông tin về thời gian.

|Cú pháp| Kích thước|Chú thích|
|--------|-----------|--------|
| DATE | giá trị từ '0001-01-01' đến '9999-12-31.| hiển thị dưới dạng ‘YYYY-MM-DD’ |
|DATETIME |Ngày lấy từ '1753-01-01 00:00:00' to '9999-12-31 23:59:59'.  Giờ lấy từ '00:00:00' to '23:59:59:997'|hiển thị dưới dạng ‘YYYY-MM-DD hh:mm:ss[.mmm]|
|DATETIME2(chính xác tới số thập phân của giây)|giá trị lấy từ '0001-01-01' đến '9999-12-31'.  Thời gian lấy từ '00:00:00' đến '23:59:59:9999999'.|hiển thị dưới dạng 'YYYY-MM-DD hh:mm:ss[.số giây thập phân]'|
|SMALLDATETIME|giá trị lấy từ '1900-01-01' đến '2079-06-06'.  Thời gian lấy từ '00:00:00' đến '23:59:59'.|hiển thị dưới dạng 'YYYY-MM-DD hh:mm:ss|
|TIME|giá trị lấy từ '00:00:00.0000000' đến '23:59:59.9999999'.  Ngày lấy từ '0001-01-01' đến '9999-12-31'.|hiển thị dưới dạng 'YYYY-MM-DD hh:mm:ss[.nnnnnnn]'|
|DATETIMEOFFSET (chính xác tới số thập phân của giây) |giá trị thời gian lấy từ '00:00:00' đến '23:59:59:9999999'.  Múi giờ lấy từ -14:00 đến +14:00.|hiển thị dưới dạng YYYY-MM-DD hh:mm:ss[.nnnnnnn]' [{+|-}hh:mm]|

---

## 🔍 2. Kiểm tra dữ liệu  

### 2.1. Xác định các loại dữ liệu có trong bảng  
- Dùng **INFORMATION_SCHEMA.COLUMNS** để kiểm tra kiểu dữ liệu của bảng.  
```sql
SELECT COLUMN_NAME, DATA_TYPE 
FROM INFORMATION_SCHEMA.COLUMNS 
WHERE TABLE_NAME = 'YourTable';
```
📌 Câu lệnh trên giúp kiểm tra tên cột và loại dữ liệu của từng cột trong bảng 'YourTable'.  

### 2.2. Kiểm tra dữ liệu NULL trong bảng  
- Sử dụng **IS NULL** để tìm giá trị NULL.  
```sql
SELECT * FROM YourTable WHERE ColumnName IS NULL;
```
📌 Truy vấn này sẽ trả về tất cả các hàng trong bảng 'YourTable' mà cột 'ColumnName' có giá trị NULL.  

---

## 🛠 3. Các hàm làm việc với kiểu dữ liệu  

### 3.1. Hàm chuyển đổi kiểu dữ liệu  
* Dùng để chuyển đổi kiểu dữ liệu giữa các loại khác nhau.
#### CAST()
* CAST cho phép chuyển đổi một kiểu dữ liệu sang một kiểu khác.
- **Ví dụ:**
```sql
SELECT CAST(123.45 AS INT) AS ConvertedValue;
SELECT CAST('2024-01-31' AS DATE) AS ConvertedDate;
```
📌 CAST(123.45 AS INT) chuyển đổi số thực 123.45 thành số nguyên 123.  
📌 CAST('2024-01-31' AS DATE) chuyển đổi chuỗi thành kiểu ngày.  
#### CONVERT()
* CONVERT được sử dụng để chuyển đổi kiểu dữ liệu, đặc biệt hữu ích cho việc chuyển đổi ngày tháng sang chuỗi theo nhiều định dạng khác nhau.
- **Ví dụ:**
```sql
SELECT CONVERT(VARCHAR, GETDATE(), 103) AS FormattedDate;
SELECT CONVERT(INT, 456.78) AS ConvertedInteger;
```
📌 CONVERT(VARCHAR, GETDATE(), 103) chuyển đổi ngày hiện tại thành chuỗi có định dạng dd/MM/yyyy.  
📌 CONVERT(INT, 456.78) chuyển đổi số thực thành số nguyên 456.  
#### TRY_CAST()
* TRY_CAST tương tự CAST, nhưng trả về NULL nếu không thể chuyển đổi được.
- **Ví dụ:**
```sql
SELECT TRY_CAST('123abc' AS INT) AS TryCastResult;
SELECT TRY_CAST('2024-01-31' AS DATE) AS TryCastDate;
```
#### TRY_CONVERT()
* TRY_CONVERT hoạt động giống CONVERT, nhưng trả về NULL nếu chuyển đổi không hợp lệ.
- **Ví dụ:**
```sql
SELECT TRY_CONVERT(INT, '456xyz') AS TryConvertResult;
SELECT TRY_CONVERT(DATE, '31-01-2024', 103) AS TryConvertDate;
```
### 3.2. Xử lý dữ liệu dạng chuỗi 
* Các hàm hỗ trợ xử lý chuỗi trong SQL.
#### CONCAT()
* Nối hai hoặc nhiều chuỗi lại với nhau.
- **Ví dụ:**
```sql
SELECT CONCAT('Hello', ' ', 'World') AS ConcatenatedString;
```
#### CONCAT_WS()
* Nối chuỗi với ký tự phân cách.
- **Ví dụ:**
```sql
SELECT CONCAT_WS('-', '2024', '01', '31') AS FormattedDate;
```
### LEN()
* Trả về độ dài của chuỗi.
- **Ví dụ:**
```sql
SELECT LEN('Hello World') AS StringLength;
```
### LEFT & RIGHT()
* Lấy một số ký tự bên trái hoặc bên phải của chuỗi.
- **Ví dụ:**
```sql
SELECT LEFT('Hello World', 5) AS LeftString;
SELECT RIGHT('Hello World', 5) AS RightString;
```
#### REPLICATE()
* Lặp lại chuỗi nhiều lần.
- **Ví dụ:**
```sql
SELECT REPLICATE('*', 5) AS RepeatedString;
```
#### REPLACE()
* Thay thế một phần của chuỗi bằng một chuỗi khác.
- **Ví dụ:**
```sql
SELECT REPLACE('Hello World', 'World', 'SQL') AS ReplacedString;
```
#### UPPER & LOWER()
* Chuyển đổi chuỗi thành chữ hoa hoặc chữ thường.
- **Ví dụ:**
```sql
SELECT UPPER('hello world') AS UpperString;
SELECT LOWER('HELLO WORLD') AS LowerString;
```
#### CHARINDEX()
* Tìm vị trí của một chuỗi con trong chuỗi cha.
- **Ví dụ:**
```sql
SELECT CHARINDEX('o', 'Hello World') AS CharPosition;
```
#### SUBSTRING()
* Trích xuất một phần của chuỗi.
- **Ví dụ:**
```sql
SELECT SUBSTRING('Hello World', 1, 5) AS SubStringResult;
```
#### LENGTH(), CONCAT(), SUBSTRING(), TRIM() – Dùng để thao tác với chuỗi.
- **Ví dụ:**
```sql
SELECT CONCAT(FirstName, ' ', LastName) AS FullName FROM Employees;
```
📌 Câu lệnh trên ghép hai cột FirstName và LastName thành một chuỗi đầy đủ.  

### 3.3. Xử lý dữ liệu dạng ngày tháng  
#### DATEDIFF()
* Tính khoảng cách giữa hai ngày.
- **Ví dụ:**
```sql
SELECT DATEDIFF(YEAR, '2000-01-01', GETDATE()) AS Age;
```
#### DATEADD()
* Thêm hoặc bớt khoảng thời gian vào một ngày.
- **Ví dụ:**
```sql
SELECT DATEADD(DAY, 7, GETDATE()) AS NextWeek;
```
#### FORMAT()
* Định dạng ngày tháng theo kiểu mong muốn.
- **Ví dụ:**
```sql
SELECT FORMAT(GETDATE(), 'dd/MM/yyyy') AS FormattedDate;
```
### 3.4. Xử lý dữ liệu NULL  
- **COALESCE(), ISNULL()** – Thay thế giá trị NULL.  
- **Ví dụ:**  
```sql
SELECT COALESCE(Address, 'Không có địa chỉ') AS Address FROM Customers;
```
📌 Nếu Address có giá trị NULL, kết quả sẽ hiển thị 'Không có địa chỉ' thay thế.  

---

## 🎨 4. Các hàm định dạng dữ liệu  

### 4.1. Định dạng ngày  
- **FORMAT()** – Chuyển đổi định dạng ngày tháng.  
- **Ví dụ:**  
```sql
SELECT FORMAT(GETDATE(), 'dd/MM/yyyy') AS FormattedDate;
```
📌 Chuyển đổi ngày hiện tại thành định dạng dd/MM/yyyy.  

### 4.2. Làm tròn số  
- **ROUND(), CEILING(), FLOOR()**  
- **Ví dụ:**  
```sql
SELECT ROUND(123.456, 2) AS RoundedValue;
SELECT CEILING(123.456) AS CeilValue;
SELECT FLOOR(123.456) AS FloorValue;
```
📌 ROUND(123.456, 2) làm tròn số 123.456 đến hai chữ số thập phân (123.46).  
📌 CEILING(123.456) làm tròn lên số nguyên gần nhất (124).  
📌 FLOOR(123.456) làm tròn xuống số nguyên gần nhất (123).  

---
### NỘI DUNG: Bùi Trịnh Minh Ngọc
