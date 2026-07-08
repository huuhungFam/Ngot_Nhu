# Bài tập SQL MySQL trong 7 ngày

Hướng dẫn:

- Điền câu trả lời SQL vào phần `Đáp án của tôi`.
- Mỗi ngày có 15 câu bài tập đa dạng (viết query, tìm lỗi sai, đọc hiểu logic).
- Các bài tập dùng bộ bảng giả định bên dưới. Bạn có thể tạo bảng thật trong MySQL hoặc chỉ viết truy vấn ra file này.

## Bộ bảng giả định

Dưới đây là một vài dòng dữ liệu mẫu (Mock Data) để bạn dễ hình dung kết quả trước khi viết code:

**Bảng `customers`:**
| customer_id | customer_name | city | segment | created_at |
|---|---|---|---|---|
| 101 | Nguyễn Văn A | Hà Nội | VIP | 2026-01-01 |
| 102 | Trần Thị B | HCM | Normal | 2026-01-15 |

**Bảng `transactions`:**
| transaction_id | customer_id | account_id | transaction_date | amount | status |
|---|---|---|---|---|---|
| 1 | 101 | 10 | 2026-01-02 | 1500000 | approved |
| 2 | 102 | 11 | 2026-01-20 | 300000 | pending |
| 3 | 101 | 10 | 2026-01-25 | 2000000 | approved |

Cấu trúc bảng chi tiết:

```sql
customers(
    customer_id INT,
    customer_name VARCHAR(100),
    city VARCHAR(100),
    segment VARCHAR(50),
    created_at DATE
)

accounts(
    account_id INT,
    account_name VARCHAR(100),
    department VARCHAR(100)
)

transactions(
    transaction_id INT,
    customer_id INT,
    account_id INT,
    transaction_date DATE,
    amount DECIMAL(15, 2),
    status VARCHAR(30)
)
```

Trạng thái giao dịch giả định:
- `approved`: đã duyệt.
- `pending`: chờ xử lý.
- `cancelled`: đã hủy.
- `review`: cần kiểm tra.

---

## Ngày 1: SELECT, WHERE, ORDER BY, LIMIT

### Câu 1
Lấy tất cả các cột trong bảng `customers`.
Đáp án của tôi:
```sql

```

### Câu 2
Lấy `customer_id`, `customer_name`, `city` trong bảng `customers`.
Đáp án của tôi:
```sql

```

### Câu 3
Lấy 10 giao dịch đầu tiên trong bảng `transactions`.
Đáp án của tôi:
```sql

```

### Câu 4
Lấy các giao dịch có `amount` lớn hơn 1,000,000.
Đáp án của tôi:
```sql

```

### Câu 5
Lấy các giao dịch có `status` là `approved`.
Đáp án của tôi:
```sql

```

### Câu 6
Lấy các giao dịch có `status` là `approved`, sắp xếp theo `amount` giảm dần.
Đáp án của tôi:
```sql

```

### Câu 7
Lấy `transaction_id`, `customer_id`, `amount` của 5 giao dịch có số tiền lớn nhất.
Đáp án của tôi:
```sql

```

### Câu 8
Lấy danh sách khách hàng (chỉ lấy tên và phân khúc `segment`), sắp xếp theo phân khúc theo bảng chữ cái.
Đáp án của tôi:
```sql

```

### Câu 9
Lấy 3 giao dịch có `amount` nhỏ nhất.
Đáp án của tôi:
```sql

```

### Câu 10
Lấy `transaction_id`, `status` của các giao dịch bị hủy (`cancelled`), sắp xếp theo ngày giao dịch mới nhất.
Đáp án của tôi:
```sql

```

### Câu 11 (Tìm lỗi sai)
Đoạn code sau muốn lấy 5 khách hàng đầu tiên trong bảng, lỗi ở đâu?
```sql
SELECT 5 * FROM customers;
```
Đáp án của tôi:
```text

```

### Câu 12 (Tìm lỗi sai)
Code sau muốn lấy giao dịch có tiền lớn hơn 500k và sắp xếp giảm dần, lỗi cú pháp nằm ở đâu?
```sql
SELECT transaction_id, amount
ORDER BY amount DESC
FROM transactions
WHERE amount > 500000;
```
Đáp án của tôi:
```text

```

### Câu 13 (Đọc hiểu)
Câu lệnh `SELECT * FROM accounts LIMIT 1;` sẽ trả về dữ liệu gì nếu bảng có 100 dòng?
Đáp án của tôi:
```text

```

### Câu 14
Viết lệnh lấy tất cả phòng ban (`department`) có trong bảng `accounts`. (Mẹo: Có thể dùng `DISTINCT` để loại bỏ trùng lặp nếu bạn đã biết, hoặc cứ SELECT bình thường).
Đáp án của tôi:
```sql

```

### Câu 15
Chỉ lấy cột `customer_name` và hiển thị nó dưới tên cột là `Ten_Khach_Hang` (dùng ALIAS).
Đáp án của tôi:
```sql

```

---

## Ngày 2: Điều kiện lọc, NULL và kiểu dữ liệu

### Câu 1
Lấy các giao dịch trong tháng 1 năm 2026 (viết điều kiện chuẩn cho `DATE`).
Đáp án của tôi:
```sql

```

### Câu 2
Lấy các giao dịch có `status` là `pending` hoặc `review`.
Đáp án của tôi:
```sql

```

### Câu 3
Lấy các khách hàng có tên bắt đầu bằng chữ `Nguyễn`.
Đáp án của tôi:
```sql

```

### Câu 4
Lấy các khách hàng ở thành phố `Hà Nội` và thuộc phân khúc `VIP`.
Đáp án của tôi:
```sql

```

### Câu 5
Tìm các giao dịch có `amount` bị thiếu (NULL).
Đáp án của tôi:
```sql

```

### Câu 6
Tìm các giao dịch KHÔNG bị thiếu `amount` (NOT NULL).
Đáp án của tôi:
```sql

```

### Câu 7
Lấy `transaction_id`, `amount`, và một cột mới tên `amount_clean` thay thế `NULL` bằng 0.
Đáp án của tôi:
```sql

```

### Câu 8
Tìm các giao dịch có `amount` âm hoặc bằng 0.
Đáp án của tôi:
```sql

```

### Câu 9
Lấy các khách hàng ở `HCM` nhưng KHÔNG thuộc phân khúc `VIP`.
Đáp án của tôi:
```sql

```

### Câu 10
Lấy các giao dịch có số tiền từ 1,000,000 đến 5,000,000 (Sử dụng `BETWEEN`).
Đáp án của tôi:
```sql

```

### Câu 11
Lấy các tài khoản thuộc bộ phận `Sales`, `Marketing` hoặc `IT` (Sử dụng `IN`).
Đáp án của tôi:
```sql

```

### Câu 12 (Tìm lỗi sai)
Code sau muốn lấy giao dịch bị thiếu số tiền, lỗi ở đâu?
```sql
SELECT * FROM transactions WHERE amount = NULL;
```
Đáp án của tôi:
```text

```

### Câu 13 (Tìm lỗi sai)
Đoạn code sau lấy các khách hàng tên "Trần". Nó có bắt được tên "Trần Thị B" không? Tại sao?
```sql
SELECT * FROM customers WHERE customer_name LIKE 'Trần_';
```
Đáp án của tôi:
```text

```

### Câu 14 (Đọc hiểu)
Câu điều kiện `WHERE amount > 100 AND status = 'pending' OR status = 'review'` có lấy nhầm giao dịch `review` nhưng `amount` bằng 0 không? Tại sao?
Đáp án của tôi:
```text

```

### Câu 15
Sửa lại câu 14 bằng cách dùng dấu ngoặc đơn để lấy đúng giao dịch (`pending` hoặc `review`) và có `amount > 100`.
Đáp án của tôi:
```sql

```

---

## Ngày 3: GROUP BY và hàm tổng hợp

### Câu 1
Đếm tổng số giao dịch trong bảng `transactions`.
Đáp án của tôi:
```sql

```

### Câu 2
Tính tổng `amount` của tất cả giao dịch có trạng thái `approved`.
Đáp án của tôi:
```sql

```

### Câu 3
Tính số giao dịch và tổng tiền theo từng `customer_id`.
Đáp án của tôi:
```sql

```

### Câu 4
Tính tổng tiền, số tiền lớn nhất, nhỏ nhất, và trung bình theo từng ngày giao dịch.
Đáp án của tôi:
```sql

```

### Câu 5
Đếm số khách hàng theo từng `city`.
Đáp án của tôi:
```sql

```

### Câu 6
Đếm số khách hàng theo từng tổ hợp `city` và `segment`.
Đáp án của tôi:
```sql

```

### Câu 7
Tìm các `customer_id` có tổng `amount` lớn hơn 10,000,000.
Đáp án của tôi:
```sql

```

### Câu 8
Tìm các ngày giao dịch có nhiều hơn 50 giao dịch.
Đáp án của tôi:
```sql

```

### Câu 9
Tính tổng `amount` theo từng `status`.
Đáp án của tôi:
```sql

```

### Câu 10
Chỉ tính tổng `amount` cho các giao dịch trong tháng 1/2026, nhóm theo `status`.
Đáp án của tôi:
```sql

```

### Câu 11
Tìm các `account_id` có tổng số tiền giao dịch âm (tổng amount < 0).
Đáp án của tôi:
```sql

```

### Câu 12 (Tìm lỗi sai)
Code sau tính tổng tiền theo trạng thái. Bị lỗi cú pháp ở đâu?
```sql
SELECT status, SUM(amount)
FROM transactions
HAVING status = 'approved'
GROUP BY status;
```
Đáp án của tôi:
```text

```

### Câu 13 (Tìm lỗi sai)
Đoạn code sau gom nhóm theo `customer_id`, lỗi ở đâu?
```sql
SELECT customer_id, transaction_date, SUM(amount)
FROM transactions
GROUP BY customer_id;
```
Đáp án của tôi:
```text

```

### Câu 14 (Đọc hiểu)
Hàm `COUNT(amount)` khác gì `COUNT(*)` nếu cột amount có dòng bị NULL?
Đáp án của tôi:
```text

```

### Câu 15
Hiển thị tổng doanh thu đã duyệt (`approved`) theo tháng. Giả định bạn dùng hàm `DATE_FORMAT(transaction_date, '%Y-%m')` làm cột tháng.
Đáp án của tôi:
```sql

```

---

## Ngày 4: JOIN

### Câu 1
Nối bảng `customers` và `transactions` để lấy `customer_name`, `transaction_id`, `transaction_date`, `amount`.
Đáp án của tôi:
```sql

```

### Câu 2
Lấy danh sách TẤT CẢ khách hàng và giao dịch của họ nếu có (Khách chưa có giao dịch vẫn lấy).
Đáp án của tôi:
```sql

```

### Câu 3
Tìm các khách hàng chưa từng phát sinh giao dịch nào.
Đáp án của tôi:
```sql

```

### Câu 4
Nối `transactions` với `accounts` để lấy tên tài khoản và phòng ban của mỗi giao dịch.
Đáp án của tôi:
```sql

```

### Câu 5
Tính tổng `amount` theo từng `department` trong bảng `accounts`.
Đáp án của tôi:
```sql

```

### Câu 6
Tìm các giao dịch tham chiếu đến một `customer_id` KHÔNG tồn tại trong bảng `customers`.
Đáp án của tôi:
```sql

```

### Câu 7
Nối cả 3 bảng để lấy: `transaction_id`, `customer_name`, `department`, `amount`.
Đáp án của tôi:
```sql

```

### Câu 8
Tính tổng `amount` theo từng `city` của khách hàng, chỉ lấy các giao dịch `approved`.
Đáp án của tôi:
```sql

```

### Câu 9
Lấy danh sách các tài khoản (`account_name`) chưa có giao dịch nào được ghi nhận.
Đáp án của tôi:
```sql

```

### Câu 10
Lấy `customer_name`, tổng số lượng giao dịch, tổng tiền của từng khách hàng.
Đáp án của tôi:
```sql

```

### Câu 11
Chỉ lấy các khách hàng ở `Hà Nội` và có tổng số tiền `approved` lớn hơn 5,000,000. Lấy cả tên khách hàng.
Đáp án của tôi:
```sql

```

### Câu 12 (Tìm lỗi sai)
Code sau muốn lấy danh sách tất cả khách hàng, dù có giao dịch hay không, nhưng lại bị mất khách hàng không có giao dịch. Lỗi ở đâu?
```sql
SELECT c.customer_name, t.amount
FROM customers AS c
INNER JOIN transactions AS t ON c.customer_id = t.customer_id;
```
Đáp án của tôi:
```text

```

### Câu 13 (Tìm lỗi sai)
Tìm khách hàng chưa có giao dịch, lỗi cú pháp ở đâu?
```sql
SELECT c.*
FROM customers c
LEFT JOIN transactions t ON c.customer_id = t.customer_id
WHERE t.transaction_id = NULL;
```
Đáp án của tôi:
```text

```

### Câu 14 (Đọc hiểu)
Nếu bảng `accounts` có 2 dòng trùng `account_id = 10`. Một giao dịch trong `transactions` có `account_id = 10`. Khi INNER JOIN 2 bảng, giao dịch này sẽ biến thành mấy dòng?
Đáp án của tôi:
```text

```

### Câu 15
Đếm số khách hàng thuộc từng `department` đã từng giao dịch với. Mỗi KH chỉ đếm 1 lần cho mỗi phòng ban. (Gợi ý dùng `COUNT(DISTINCT customer_id)`).
Đáp án của tôi:
```sql

```

---

## Ngày 5: Subquery và CTE

### Câu 1
Lấy các giao dịch có `amount` lớn hơn giá trị trung bình của toàn bộ bảng `transactions` (dùng Subquery).
Đáp án của tôi:
```sql

```

### Câu 2
Dùng CTE để tính tổng tiền theo khách hàng, sau đó từ CTE này lấy các khách hàng có tổng tiền > 10,000,000.
Đáp án của tôi:
```sql

```

### Câu 3
Dùng Subquery với `IN` để lấy danh sách khách hàng có ít nhất một giao dịch `review`.
Đáp án của tôi:
```sql

```

### Câu 4
Dùng CTE tính tổng doanh thu theo tháng (tên CTE là `monthly_sales`), sau đó select từ CTE này.
Đáp án của tôi:
```sql

```

### Câu 5
Từ CTE ở Câu 4, chỉ lọc lấy các tháng có tổng doanh thu > 50,000,000.
Đáp án của tôi:
```sql

```

### Câu 6
Dùng CTE gom nhóm theo `customer_id` (lấy số lần giao dịch approved). Từ đó lấy khách có số lần giao dịch >= 3.
Đáp án của tôi:
```sql

```

### Câu 7
Lấy giao dịch có `amount` lớn nhất hệ thống bằng Subquery.
Đáp án của tôi:
```sql

```

### Câu 8
Dùng CTE tính số lượng giao dịch theo từng ngày. Sau đó tính ngày có số giao dịch cao nhất bằng `MAX()`.
Đáp án của tôi:
```sql

```

### Câu 9
Viết truy vấn lấy các khách hàng có ngày tạo tài khoản (`created_at`) giống hệt ngày phát sinh giao dịch đầu tiên của họ. (Kết hợp Subquery và hàm MIN).
Đáp án của tôi:
```sql

```

### Câu 10
Dùng Subquery với `NOT IN` để tìm các `account_id` không có giao dịch nào.
Đáp án của tôi:
```sql

```

### Câu 11
Lấy các giao dịch có `amount` lớn hơn trung bình `amount` của TỪNG `account_id` tương ứng (Correlated subquery).
Đáp án của tôi:
```sql

```

### Câu 12 (Tìm lỗi sai)
Lấy giao dịch có số tiền lớn hơn trung bình, báo lỗi. Tại sao?
```sql
SELECT * FROM transactions
WHERE amount > (SELECT amount, AVG(amount) FROM transactions);
```
Đáp án của tôi:
```text

```

### Câu 13 (Tìm lỗi sai)
Đoạn CTE sau báo lỗi, sửa thế nào?
```sql
WITH cust_total (
    SELECT customer_id, SUM(amount) FROM transactions GROUP BY customer_id
)
SELECT * FROM cust_total;
```
Đáp án của tôi:
```text

```

### Câu 14 (Đọc hiểu)
Dùng Subquery `IN` để lọc danh sách, nếu trong danh sách subquery có chứa `NULL`, thì điều kiện `NOT IN` có hoạt động đúng không?
Đáp án của tôi:
```text

```

### Câu 15
Sử dụng CTE bọc 2 lớp: Lớp 1 tính tổng tiền mỗi khách. Lớp 2 lấy tổng tiền đó chia cho số lượng khách hàng để ra giá trị trung bình trên mỗi khách.
Đáp án của tôi:
```sql

```

---

## Ngày 6: Window functions

### Câu 1
Dùng `ROW_NUMBER()` để đánh số thứ tự giao dịch của mỗi khách hàng theo thời gian tăng dần.
Đáp án của tôi:
```sql

```

### Câu 2
Tính tổng lũy kế `amount` theo từng khách hàng, sắp xếp theo ngày giao dịch.
Đáp án của tôi:
```sql

```

### Câu 3
Tính trung bình `amount` của từng khách hàng và hiển thị cột đó trên mỗi dòng giao dịch của họ.
Đáp án của tôi:
```sql

```

### Câu 4
Xếp hạng giao dịch bằng `RANK()` theo `amount` giảm dần trong từng khách hàng.
Đáp án của tôi:
```sql

```

### Câu 5
Dùng CTE bọc hàm Window Function tính trung bình ở Câu 3, sau đó lọc lấy các giao dịch lớn hơn 3 lần trung bình của khách hàng đó.
Đáp án của tôi:
```sql

```

### Câu 6
Tìm giao dịch ĐẦU TIÊN của mỗi khách hàng. (Gợi ý bọc `ROW_NUMBER` trong CTE rồi lọc `= 1`).
Đáp án của tôi:
```sql

```

### Câu 7
Tìm giao dịch LỚN NHẤT (theo amount) của mỗi tài khoản (account_id) bằng cách dùng `ROW_NUMBER()`.
Đáp án của tôi:
```sql

```

### Câu 8
Tính tổng lũy kế doanh thu toàn công ty theo ngày giao dịch (nhóm theo ngày trước, sau đó dùng `SUM() OVER(ORDER BY)`).
Đáp án của tôi:
```sql

```

### Câu 9
Dùng `DENSE_RANK()` để xếp hạng khách hàng theo `created_at`.
Đáp án của tôi:
```sql

```

### Câu 10
Dùng hàm `LAG()` để lấy ngày giao dịch liền trước của mỗi khách hàng, đặt tên cột là `prev_transaction_date`.
Đáp án của tôi:
```sql

```

### Câu 11
Dùng `LEAD()` để lấy `amount` của giao dịch tiếp theo của cùng khách hàng.
Đáp án của tôi:
```sql

```

### Câu 12 (Tìm lỗi sai)
Query sau muốn lọc trực tiếp bằng hàm Window nhưng báo lỗi cú pháp. Lỗi ở đâu?
```sql
SELECT *, ROW_NUMBER() OVER(PARTITION BY customer_id) AS rn
FROM transactions
WHERE ROW_NUMBER() OVER(PARTITION BY customer_id) = 1;
```
Đáp án của tôi:
```text

```

### Câu 13 (Tìm lỗi sai)
Query tính tổng lũy kế nhưng lại ra kết quả tổng chung cho cả bảng trên mọi dòng. Nó thiếu mệnh đề gì trong hàm OVER?
```sql
SELECT amount, SUM(amount) OVER() FROM transactions;
```
Đáp án của tôi:
```text

```

### Câu 14 (Đọc hiểu)
Sự khác biệt khi có 2 dòng đồng hạng 1 giữa `RANK()` và `DENSE_RANK()` là gì? Hạng tiếp theo sẽ là số mấy?
Đáp án của tôi:
```text

```

### Câu 15
Tính phần trăm đóng góp của mỗi giao dịch so với tổng giao dịch của khách hàng đó (Gợi ý: `amount / SUM(amount) OVER(...)`).
Đáp án của tôi:
```sql

```

---

## Ngày 7: Chất lượng dữ liệu và Mini project

### Câu 1
Kiểm đếm số giao dịch và tổng tiền của từng `status` để rà soát dữ liệu.
Đáp án của tôi:
```sql

```

### Câu 2
Tìm các giao dịch có số tiền bất thường (`amount < 0` hoặc `amount > 1,000,000,000`).
Đáp án của tôi:
```sql

```

### Câu 3
Tìm các giao dịch không có `customer_id` hợp lệ.
Đáp án của tôi:
```sql

```

### Câu 4
Đếm số lượng giá trị `NULL` trong cột `amount` của bảng `transactions`.
Đáp án của tôi:
```sql

```

### Câu 5
Tạo bảng `transactions_audit` (DDL) với các cột `audit_id` (Tự động tăng, Khóa chính), `transaction_id`, `reason`, `created_at`.
Đáp án của tôi:
```sql

```

### Câu 6
Sử dụng lệnh `INSERT INTO ... SELECT` để đẩy các giao dịch có `amount < 0` vào bảng `transactions_audit`, cột reason ghi 'Negative amount'.
Đáp án của tôi:
```sql

```

### Câu 7
Viết lệnh `UPDATE` để chuyển các giao dịch có `amount < 0` thành trạng thái `review`.
Đáp án của tôi:
```sql

```

### Câu 8
Viết lệnh `DELETE` xóa các giao dịch thuộc trạng thái `cancelled` đã cũ (trước năm 2020).
Đáp án của tôi:
```sql

```

### Câu 9
[Mini Project] Lập báo cáo Tổng doanh thu `approved` theo Tháng. Gồm: Tháng, Tổng tiền, Số giao dịch, Trung bình/giao dịch.
Đáp án của tôi:
```sql

```

### Câu 10
[Mini Project] Top 10 khách hàng đem lại doanh thu `approved` cao nhất (Cần JOIN để lấy Tên khách hàng và Thành phố).
Đáp án của tôi:
```sql

```

### Câu 11
[Mini Project] Báo cáo rủi ro: Lấy danh sách các khách hàng có tổng doanh thu `approved` > 10 triệu nhưng lại có ít nhất 1 giao dịch đang ở trạng thái `review`.
Đáp án của tôi:
```sql

```

### Câu 12
[Mini Project] Phân tích phòng ban: Tìm phòng ban (`department`) có tỷ lệ giao dịch `cancelled` cao nhất tính theo số lượng dòng.
Đáp án của tôi:
```sql

```

### Câu 13 (Tìm lỗi sai)
Đoạn lệnh cập nhật dữ liệu sau rất nguy hiểm vì quên mất điều kiện gì?
```sql
UPDATE transactions
SET status = 'approved';
```
Đáp án của tôi:
```text

```

### Câu 14 (Đọc hiểu)
Nếu bạn xóa (DELETE) một `customer` trong bảng `customers`, chuyện gì xảy ra với các dòng `transactions` của người đó nếu cơ sở dữ liệu không cài đặt `ON DELETE CASCADE`?
Đáp án của tôi:
```text

```

### Câu 15
[Mini Project] Viết 1 CTE kết hợp Window Function: Lấy giao dịch `approved` lớn nhất của mỗi khách hàng, đồng thời hiển thị kèm Tên khách hàng và Tên phòng ban (`department`) xử lý giao dịch đó.
Đáp án của tôi:
```sql

```
