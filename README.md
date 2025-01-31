# 🚀 SQLwithDAB  

## 🛢️ Tổng quan về SQL  

### 📌 1. Ngôn ngữ SQL là gì? Tóm tắt lịch sử hình thành SQL  

**SQL (Structured Query Language)** là ngôn ngữ tiêu chuẩn dùng để tương tác với hệ quản trị cơ sở dữ liệu (DBMS). SQL được sử dụng để truy vấn, chèn, cập nhật, và xóa dữ liệu cũng như quản lý cấu trúc của cơ sở dữ liệu.  

SQL được phát triển vào những năm 1970 tại IBM với tên gọi SEQUEL (Structured English Query Language). Sau đó, nó được chuẩn hóa bởi ANSI (American National Standards Institute) vào năm 1986 và ISO (International Organization for Standardization) vào năm 1987. Kể từ đó, SQL đã trở thành tiêu chuẩn chung trong quản lý cơ sở dữ liệu quan hệ.  

### 🛠️ 2. Một số hệ quản trị cơ sở dữ liệu  

**Một số hệ quản trị cơ sở dữ liệu phổ biến sử dụng SQL bao gồm:**  

* MySQL: Mã nguồn mở, phổ biến trong các ứng dụng web.  

* PostgreSQL: Hệ quản trị cơ sở dữ liệu quan hệ mạnh mẽ, hỗ trợ ACID.  

* Microsoft SQL Server: Hệ thống DBMS do Microsoft phát triển, phổ biến trong doanh nghiệp.  

* Oracle Database: Hệ thống DBMS thương mại mạnh mẽ, hỗ trợ giao dịch lớn.  

* SQLite: Hệ quản trị cơ sở dữ liệu nhẹ, thường được sử dụng trong các ứng dụng di động.  

### 📌 3. Một số khái niệm trong cơ sở dữ liệu  

#### 3.1. Cơ sở dữ liệu quan hệ (Relational Database)  

*Cơ sở dữ liệu quan hệ tổ chức dữ liệu dưới dạng bảng (table), trong đó các hàng (record) chứa dữ liệu và các cột (field) đại diện cho các thuộc tính của dữ liệu. Các bảng có thể liên kết với nhau thông qua khóa chính (Primary Key) và khóa ngoại (Foreign Key).*  

#### 3.2. Cơ sở dữ liệu phi quan hệ (NoSQL)  

Cơ sở dữ liệu phi quan hệ không lưu trữ dữ liệu dưới dạng bảng mà sử dụng các mô hình như:  

* Key-Value Store: Redis, DynamoDB  

* Document-Oriented Database: MongoDB, CouchDB  

* Column-Family Store: Apache Cassandra, HBase  

* Graph Database: Neo4j  

*NoSQL thường được sử dụng trong các hệ thống yêu cầu mở rộng cao và xử lý dữ liệu không có cấu trúc cố định.*  

### 📌 4. Các nhóm câu lệnh SQL  

SQL được chia thành các nhóm chính:  

* DDL (Data Definition Language): Quản lý cấu trúc của cơ sở dữ liệu (CREATE, ALTER, DROP).  

* DML (Data Manipulation Language): Thao tác dữ liệu (INSERT, UPDATE, DELETE).  

* DQL (Data Query Language): Truy vấn dữ liệu (SELECT).  

* DCL (Data Control Language): Quản lý quyền truy cập (GRANT, REVOKE).  

* TCL (Transaction Control Language): Quản lý giao dịch (COMMIT, ROLLBACK, SAVEPOINT).  

### 📌 5. Cách thức thực hiện câu lệnh SQL (Logical Query Processing)  

SQL được thực thi theo quy trình xử lý truy vấn logic (Logical Query Processing), trong đó thứ tự thực hiện các thành phần của câu lệnh khác với thứ tự viết. Ví dụ, một truy vấn SELECT thực hiện theo các bước:  

* FROM: Xác định bảng dữ liệu.  

* WHERE: Lọc dữ liệu theo điều kiện.  

* GROUP BY: Nhóm dữ liệu.  

* HAVING: Lọc dữ liệu nhóm.  

* SELECT: Chọn cột cần lấy dữ liệu.  

* ORDER BY: Sắp xếp dữ liệu.  

Hiểu quy trình này giúp tối ưu hóa truy vấn và viết câu lệnh SQL hiệu quả hơn.  

