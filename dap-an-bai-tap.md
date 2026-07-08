# Đáp án Bài tập SQL MySQL trong 7 ngày

## Ngày 1: SELECT, WHERE, ORDER BY, LIMIT
### Câu 1
```sql
SELECT * FROM customers;
```
### Câu 2
```sql
SELECT customer_id, customer_name, city FROM customers;
```
### Câu 3
```sql
SELECT * FROM transactions LIMIT 10;
```
### Câu 4
```sql
SELECT * FROM transactions WHERE amount > 1000000;
```
### Câu 5
```sql
SELECT * FROM transactions WHERE status = 'approved';
```
### Câu 6
```sql
SELECT * FROM transactions WHERE status = 'approved' ORDER BY amount DESC;
```
### Câu 7
```sql
SELECT transaction_id, customer_id, amount FROM transactions ORDER BY amount DESC LIMIT 5;
```
### Câu 8
```sql
SELECT customer_name, segment FROM customers ORDER BY segment ASC;
```
### Câu 9
```sql
SELECT * FROM transactions ORDER BY amount ASC LIMIT 3;
```
### Câu 10
```sql
SELECT transaction_id, status FROM transactions WHERE status = 'cancelled' ORDER BY transaction_date DESC;
```
### Câu 11
```text
Lỗi cú pháp. Lệnh LIMIT 5 phải đứng ở cuối query, không được viết cạnh SELECT. Cú pháp đúng: SELECT * FROM customers LIMIT 5;
```
### Câu 12
```text
Lỗi thứ tự các mệnh đề. Mệnh đề WHERE bắt buộc phải đứng TRƯỚC ORDER BY.
```
### Câu 13
```text
Trả về đúng 1 dòng (dòng đầu tiên quét được) từ bảng accounts, bất kể bảng có 100 hay 1 triệu dòng.
```
### Câu 14
```sql
SELECT DISTINCT department FROM accounts;
```
### Câu 15
```sql
SELECT customer_name AS Ten_Khach_Hang FROM customers;
```

## Ngày 2: Điều kiện lọc, NULL và kiểu dữ liệu
### Câu 1
```sql
SELECT * FROM transactions WHERE transaction_date >= '2026-01-01' AND transaction_date < '2026-02-01';
```
### Câu 2
```sql
SELECT * FROM transactions WHERE status IN ('pending', 'review');
```
### Câu 3
```sql
SELECT * FROM customers WHERE customer_name LIKE 'Nguyễn%';
```
### Câu 4
```sql
SELECT * FROM customers WHERE city = 'Hà Nội' AND segment = 'VIP';
```
### Câu 5
```sql
SELECT * FROM transactions WHERE amount IS NULL;
```
### Câu 6
```sql
SELECT * FROM transactions WHERE amount IS NOT NULL;
```
### Câu 7
```sql
SELECT transaction_id, amount, COALESCE(amount, 0) AS amount_clean FROM transactions;
```
### Câu 8
```sql
SELECT * FROM transactions WHERE amount <= 0;
```
### Câu 9
```sql
SELECT * FROM customers WHERE city = 'HCM' AND segment <> 'VIP';
```
### Câu 10
```sql
SELECT * FROM transactions WHERE amount BETWEEN 1000000 AND 5000000;
```
### Câu 11
```sql
SELECT * FROM accounts WHERE department IN ('Sales', 'Marketing', 'IT');
```
### Câu 12
```text
Lỗi kiểm tra NULL. Trong SQL, không được dùng toán tử `=` để so sánh với NULL. Phải dùng `IS NULL`.
```
### Câu 13
```text
Không bắt được chữ "Trần Thị B". Ký tự `_` trong hàm LIKE chỉ đại diện cho ĐÚNG 1 ký tự. Để đại diện cho chuỗi dài, phải dùng ký tự `%`. Sửa lại: LIKE 'Trần%'.
```
### Câu 14
```text
Có. Toán tử AND được ưu tiên tính trước OR. Câu này tương đương: `(amount > 100 AND status = 'pending') OR (status = 'review')`. Giao dịch review dù amount có bằng 0 vẫn lọt qua điều kiện vế sau của OR.
```
### Câu 15
```sql
SELECT * FROM transactions WHERE amount > 100 AND (status = 'pending' OR status = 'review');
```

## Ngày 3: GROUP BY và hàm tổng hợp
### Câu 1
```sql
SELECT COUNT(*) FROM transactions;
```
### Câu 2
```sql
SELECT SUM(amount) FROM transactions WHERE status = 'approved';
```
### Câu 3
```sql
SELECT customer_id, COUNT(*) AS count_trans, SUM(amount) AS total_amount FROM transactions GROUP BY customer_id;
```
### Câu 4
```sql
SELECT transaction_date, SUM(amount), MAX(amount), MIN(amount), AVG(amount) FROM transactions GROUP BY transaction_date;
```
### Câu 5
```sql
SELECT city, COUNT(*) FROM customers GROUP BY city;
```
### Câu 6
```sql
SELECT city, segment, COUNT(*) FROM customers GROUP BY city, segment;
```
### Câu 7
```sql
SELECT customer_id, SUM(amount) FROM transactions GROUP BY customer_id HAVING SUM(amount) > 10000000;
```
### Câu 8
```sql
SELECT transaction_date, COUNT(*) FROM transactions GROUP BY transaction_date HAVING COUNT(*) > 50;
```
### Câu 9
```sql
SELECT status, SUM(amount) FROM transactions GROUP BY status;
```
### Câu 10
```sql
SELECT status, SUM(amount) FROM transactions WHERE transaction_date >= '2026-01-01' AND transaction_date < '2026-02-01' GROUP BY status;
```
### Câu 11
```sql
SELECT account_id, SUM(amount) FROM transactions GROUP BY account_id HAVING SUM(amount) < 0;
```
### Câu 12
```text
Lỗi dùng HAVING thay vì WHERE. Để lọc trước khi GROUP BY, phải dùng WHERE. Còn HAVING chỉ dùng lọc sau khi tính toán.
Sửa: WHERE status = 'approved' (đặt TRƯỚC Group By).
```
### Câu 13
```text
Cột transaction_date không nằm trong lệnh GROUP BY và không được bọc bởi bất kỳ hàm tổng hợp nào. Trong SQL chuẩn, query này sẽ báo lỗi. Phải thêm transaction_date vào GROUP BY hoặc dùng hàm MIN/MAX cho nó.
```
### Câu 14
```text
COUNT(*) đếm TẤT CẢ các dòng (dù dòng đó có chứa giá trị gì đi nữa). COUNT(amount) chỉ đếm các dòng mà cột amount không bị NULL.
```
### Câu 15
```sql
SELECT DATE_FORMAT(transaction_date, '%Y-%m') AS month, SUM(amount) FROM transactions WHERE status = 'approved' GROUP BY DATE_FORMAT(transaction_date, '%Y-%m');
```

## Ngày 4: JOIN
### Câu 1
```sql
SELECT c.customer_name, t.transaction_id, t.transaction_date, t.amount
FROM transactions t JOIN customers c ON t.customer_id = c.customer_id;
```
### Câu 2
```sql
SELECT c.*, t.*
FROM customers c LEFT JOIN transactions t ON c.customer_id = t.customer_id;
```
### Câu 3
```sql
SELECT c.*
FROM customers c LEFT JOIN transactions t ON c.customer_id = t.customer_id
WHERE t.transaction_id IS NULL;
```
### Câu 4
```sql
SELECT t.transaction_id, a.account_name, a.department
FROM transactions t JOIN accounts a ON t.account_id = a.account_id;
```
### Câu 5
```sql
SELECT a.department, SUM(t.amount)
FROM transactions t JOIN accounts a ON t.account_id = a.account_id
GROUP BY a.department;
```
### Câu 6
```sql
SELECT t.*
FROM transactions t LEFT JOIN customers c ON t.customer_id = c.customer_id
WHERE c.customer_id IS NULL;
```
### Câu 7
```sql
SELECT t.transaction_id, c.customer_name, a.department, t.amount
FROM transactions t 
JOIN customers c ON t.customer_id = c.customer_id
JOIN accounts a ON t.account_id = a.account_id;
```
### Câu 8
```sql
SELECT c.city, SUM(t.amount)
FROM customers c JOIN transactions t ON c.customer_id = t.customer_id
WHERE t.status = 'approved' GROUP BY c.city;
```
### Câu 9
```sql
SELECT a.account_name
FROM accounts a LEFT JOIN transactions t ON a.account_id = t.account_id
WHERE t.transaction_id IS NULL;
```
### Câu 10
```sql
SELECT c.customer_name, COUNT(t.transaction_id), SUM(t.amount)
FROM customers c LEFT JOIN transactions t ON c.customer_id = t.customer_id
GROUP BY c.customer_id, c.customer_name;
```
### Câu 11
```sql
SELECT c.customer_name, c.city, SUM(t.amount)
FROM customers c JOIN transactions t ON c.customer_id = t.customer_id
WHERE c.city = 'Hà Nội' AND t.status = 'approved'
GROUP BY c.customer_id, c.customer_name, c.city
HAVING SUM(t.amount) > 5000000;
```
### Câu 12
```text
Dùng INNER JOIN chỉ lấy phần giao chung. Người chưa có giao dịch không nằm ở phần chung nên bị loại. Sửa lại: Dùng LEFT JOIN.
```
### Câu 13
```text
Phép gán = NULL không hợp lệ trong SQL. Phải dùng `IS NULL`. Sửa lại: WHERE t.transaction_id IS NULL.
```
### Câu 14
```text
Sẽ bị nhân bản thành 2 dòng. Đây là lỗi cực kỳ nguy hiểm khiến tổng doanh thu SUM(amount) bị nhân đôi. Khóa của bảng bị JOIN vào bắt buộc phải duy nhất (Unique).
```
### Câu 15
```sql
SELECT a.department, COUNT(DISTINCT t.customer_id)
FROM transactions t JOIN accounts a ON t.account_id = a.account_id
GROUP BY a.department;
```

## Ngày 5: Subquery và CTE
### Câu 1
```sql
SELECT * FROM transactions WHERE amount > (SELECT AVG(amount) FROM transactions);
```
### Câu 2
```sql
WITH CustTotal AS (
    SELECT customer_id, SUM(amount) AS total_amount FROM transactions GROUP BY customer_id
)
SELECT * FROM CustTotal WHERE total_amount > 10000000;
```
### Câu 3
```sql
SELECT * FROM customers WHERE customer_id IN (SELECT customer_id FROM transactions WHERE status = 'review');
```
### Câu 4
```sql
WITH monthly_sales AS (
    SELECT DATE_FORMAT(transaction_date, '%Y-%m') AS month, SUM(amount) AS total_amount
    FROM transactions GROUP BY DATE_FORMAT(transaction_date, '%Y-%m')
)
SELECT * FROM monthly_sales;
```
### Câu 5
```sql
WITH monthly_sales AS (
    SELECT DATE_FORMAT(transaction_date, '%Y-%m') AS month, SUM(amount) AS total_amount
    FROM transactions GROUP BY DATE_FORMAT(transaction_date, '%Y-%m')
)
SELECT * FROM monthly_sales WHERE total_amount > 50000000;
```
### Câu 6
```sql
WITH CustCount AS (
    SELECT customer_id, COUNT(*) AS txn_count FROM transactions WHERE status = 'approved' GROUP BY customer_id
)
SELECT * FROM CustCount WHERE txn_count >= 3;
```
### Câu 7
```sql
SELECT * FROM transactions WHERE amount = (SELECT MAX(amount) FROM transactions);
```
### Câu 8
```sql
WITH DailyCount AS (
    SELECT transaction_date, COUNT(*) AS c FROM transactions GROUP BY transaction_date
)
SELECT transaction_date, c FROM DailyCount WHERE c = (SELECT MAX(c) FROM DailyCount);
```
### Câu 9
```sql
SELECT c.*
FROM customers c 
WHERE c.created_at = (SELECT MIN(transaction_date) FROM transactions t WHERE t.customer_id = c.customer_id);
```
### Câu 10
```sql
SELECT * FROM accounts WHERE account_id NOT IN (SELECT account_id FROM transactions WHERE account_id IS NOT NULL);
```
### Câu 11
```sql
SELECT t1.*
FROM transactions t1
WHERE t1.amount > (SELECT AVG(t2.amount) FROM transactions t2 WHERE t2.account_id = t1.account_id);
```
### Câu 12
```text
Subquery trả về 2 cột (amount và AVG). Phép toán `>` yêu cầu Subquery bên phải chỉ được phép trả về 1 cột và 1 dòng duy nhất.
```
### Câu 13
```text
Lỗi khai báo CTE. CTE phải được viết bằng định dạng `WITH ten_cte AS (SELECT...)`. Bỏ chữ AS đi là sai cú pháp. Sửa: WITH cust_total AS (...)
```
### Câu 14
```text
Không hoạt động đúng. NOT IN sẽ so sánh từng phần tử. Trả về `1 NOT IN (2, 3, NULL)` sẽ được hiểu là `(1 <> 2) AND (1 <> 3) AND (1 <> NULL)`. Vì `1 <> NULL` trả về giá trị UNKNOWN (không rõ ràng), nên toàn bộ câu NOT IN sẽ không trả về dòng nào.
```
### Câu 15
```sql
WITH CustTotal AS (
    SELECT customer_id, SUM(amount) as s FROM transactions GROUP BY customer_id
),
AvgTotal AS (
    SELECT SUM(s)/COUNT(*) as avg_per_cust FROM CustTotal
)
SELECT * FROM AvgTotal;
```

## Ngày 6: Window functions
### Câu 1
```sql
SELECT customer_id, transaction_id, transaction_date, ROW_NUMBER() OVER(PARTITION BY customer_id ORDER BY transaction_date) AS rn
FROM transactions;
```
### Câu 2
```sql
SELECT customer_id, transaction_date, amount, SUM(amount) OVER(PARTITION BY customer_id ORDER BY transaction_date, transaction_id) AS run_tot
FROM transactions;
```
### Câu 3
```sql
SELECT customer_id, transaction_id, amount, AVG(amount) OVER(PARTITION BY customer_id) AS avg_amt
FROM transactions;
```
### Câu 4
```sql
SELECT customer_id, transaction_id, amount, RANK() OVER(PARTITION BY customer_id ORDER BY amount DESC) AS rnk
FROM transactions;
```
### Câu 5
```sql
WITH TxnAvg AS (
    SELECT *, AVG(amount) OVER(PARTITION BY customer_id) AS avg_amt FROM transactions
)
SELECT * FROM TxnAvg WHERE amount > 3 * avg_amt;
```
### Câu 6
```sql
WITH TxnRn AS (
    SELECT *, ROW_NUMBER() OVER(PARTITION BY customer_id ORDER BY transaction_date, transaction_id) AS rn FROM transactions
)
SELECT * FROM TxnRn WHERE rn = 1;
```
### Câu 7
```sql
WITH TxnRn AS (
    SELECT *, ROW_NUMBER() OVER(PARTITION BY account_id ORDER BY amount DESC, transaction_id) AS rn FROM transactions
)
SELECT * FROM TxnRn WHERE rn = 1;
```
### Câu 8
```sql
WITH DailySum AS (
    SELECT transaction_date, SUM(amount) AS d_sum FROM transactions GROUP BY transaction_date
)
SELECT transaction_date, d_sum, SUM(d_sum) OVER(ORDER BY transaction_date) AS running_total FROM DailySum;
```
### Câu 9
```sql
SELECT customer_id, created_at, DENSE_RANK() OVER(ORDER BY created_at) AS rnk FROM customers;
```
### Câu 10
```sql
SELECT customer_id, transaction_date, LAG(transaction_date) OVER(PARTITION BY customer_id ORDER BY transaction_date) AS prev_transaction_date
FROM transactions;
```
### Câu 11
```sql
SELECT customer_id, transaction_date, amount, LEAD(amount) OVER(PARTITION BY customer_id ORDER BY transaction_date) AS next_amount
FROM transactions;
```
### Câu 12
```text
Lỗi dùng trực tiếp Window Function trong mệnh đề WHERE. SQL không cho phép việc này vì thứ tự thực thi WHERE diễn ra trước khi tính Window. Cần bọc vào CTE (hoặc subquery) rồi lọc ở query bên ngoài.
```
### Câu 13
```text
Cú pháp tính tổng lũy kế bắt buộc phải có ORDER BY bên trong mệnh đề OVER(). Vì thiếu ORDER BY, SUM() OVER() sẽ tính tổng toàn bộ bảng lên tất cả các dòng thay vì cộng dồn từng dòng.
```
### Câu 14
```text
RANK(): nếu có 2 dòng đồng hạng 1, hạng tiếp theo bị đẩy xuống số 3 (bỏ qua số 2).
DENSE_RANK(): nếu có 2 dòng đồng hạng 1, hạng tiếp theo vẫn là số 2 (mật độ dày, không bị bỏ trống).
```
### Câu 15
```sql
SELECT customer_id, transaction_id, amount, (amount / SUM(amount) OVER(PARTITION BY customer_id)) * 100 AS pct_contribution
FROM transactions;
```

## Ngày 7: Chất lượng dữ liệu và Mini project
### Câu 1
```sql
SELECT status, COUNT(*), SUM(amount) FROM transactions GROUP BY status;
```
### Câu 2
```sql
SELECT * FROM transactions WHERE amount < 0 OR amount > 1000000000;
```
### Câu 3
```sql
SELECT t.* FROM transactions t LEFT JOIN customers c ON t.customer_id = c.customer_id WHERE c.customer_id IS NULL;
```
### Câu 4
```sql
SELECT COUNT(*) FROM transactions WHERE amount IS NULL;
```
### Câu 5
```sql
CREATE TABLE transactions_audit (
    audit_id INT AUTO_INCREMENT PRIMARY KEY,
    transaction_id INT,
    reason VARCHAR(255),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```
### Câu 6
```sql
INSERT INTO transactions_audit (transaction_id, reason)
SELECT transaction_id, 'Negative amount' FROM transactions WHERE amount < 0;
```
### Câu 7
```sql
UPDATE transactions SET status = 'review' WHERE amount < 0;
```
### Câu 8
```sql
DELETE FROM transactions WHERE status = 'cancelled' AND transaction_date < '2020-01-01';
```
### Câu 9
```sql
SELECT DATE_FORMAT(transaction_date, '%Y-%m') AS month, SUM(amount) AS total_revenue, COUNT(*) AS txn_count, AVG(amount) AS avg_txn
FROM transactions WHERE status = 'approved' GROUP BY DATE_FORMAT(transaction_date, '%Y-%m') ORDER BY month;
```
### Câu 10
```sql
SELECT c.customer_id, c.customer_name, c.city, SUM(t.amount) AS total_rev
FROM customers c JOIN transactions t ON c.customer_id = t.customer_id
WHERE t.status = 'approved' GROUP BY c.customer_id, c.customer_name, c.city
ORDER BY total_rev DESC LIMIT 10;
```
### Câu 11
```sql
WITH RevTotal AS (
    SELECT customer_id, SUM(amount) AS tot FROM transactions WHERE status = 'approved' GROUP BY customer_id HAVING SUM(amount) > 10000000
),
HasReview AS (
    SELECT DISTINCT customer_id FROM transactions WHERE status = 'review'
)
SELECT c.*, r.tot FROM customers c JOIN RevTotal r ON c.customer_id = r.customer_id JOIN HasReview h ON c.customer_id = h.customer_id;
```
### Câu 12
```sql
WITH DeptCount AS (
    SELECT a.department, 
           COUNT(*) AS total_txn, 
           SUM(CASE WHEN t.status = 'cancelled' THEN 1 ELSE 0 END) AS cancel_txn
    FROM transactions t JOIN accounts a ON t.account_id = a.account_id
    GROUP BY a.department
)
SELECT department, (cancel_txn * 100.0 / total_txn) AS cancel_rate FROM DeptCount ORDER BY cancel_rate DESC LIMIT 1;
```
### Câu 13
```text
Cực kỳ nguy hiểm vì thiếu mệnh đề WHERE. Câu lệnh này sẽ quét toàn bộ bảng và đổi toàn bộ dữ liệu thành `approved`, làm hỏng toàn bộ lịch sử trạng thái của hệ thống.
```
### Câu 14
```text
Các giao dịch (transactions) thuộc khách hàng bị xóa vẫn sẽ nằm lại trong bảng transactions (trở thành dữ liệu mồ côi - orphan rows) nhưng cột customer_id của nó trỏ vào khoảng không. Khi JOIN bảng sẽ không ra dữ liệu. Để ngăn chặn, Database thiết kế Ràng buộc Khóa Ngoại (Foreign Key Constraint) để cấm xóa hoặc dùng CASCADE.
```
### Câu 15
```sql
WITH MaxTxn AS (
    SELECT t.*, ROW_NUMBER() OVER(PARTITION BY t.customer_id ORDER BY t.amount DESC) as rn
    FROM transactions t WHERE t.status = 'approved'
)
SELECT m.transaction_id, c.customer_name, a.department, m.amount
FROM MaxTxn m 
JOIN customers c ON m.customer_id = c.customer_id
JOIN accounts a ON m.account_id = a.account_id
WHERE m.rn = 1;
```
