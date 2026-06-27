# Đáp án Bài tập SQL MySQL trong 7 ngày

## Ngày 1: SELECT, WHERE, ORDER BY, LIMIT
(Các đáp án ngày 1 đã được cung cấp trong file bài tập)

## Ngày 2: Điều kiện lọc, NULL và kiểu dữ liệu
### Câu 1
```sql
SELECT *
FROM transactions
WHERE transaction_date >= '2026-01-01' AND transaction_date < '2026-02-01';
```
### Câu 2
```sql
SELECT *
FROM transactions
WHERE status IN ('pending', 'review');
```
### Câu 3
```sql
SELECT *
FROM customers
WHERE customer_name LIKE 'Nguyễn%';
```
### Câu 4
```sql
SELECT *
FROM transactions
WHERE amount IS NULL;
```
### Câu 5
```sql
SELECT transaction_id, amount, COALESCE(amount, 0) AS amount_clean
FROM transactions;
```
### Câu 6
```sql
SELECT *
FROM transactions
WHERE amount <= 0;
```

## Ngày 3: GROUP BY và hàm tổng hợp
### Câu 1
```sql
SELECT COUNT(*) AS total_transactions
FROM transactions;
```
### Câu 2
```sql
SELECT SUM(amount) AS total_approved_amount
FROM transactions
WHERE status = 'approved';
```
### Câu 3
```sql
SELECT customer_id, COUNT(*) AS transaction_count, SUM(amount) AS total_amount
FROM transactions
GROUP BY customer_id;
```
### Câu 4
```sql
SELECT transaction_date, SUM(amount) AS daily_amount
FROM transactions
GROUP BY transaction_date;
```
### Câu 5
```sql
SELECT customer_id, SUM(amount) AS total_amount
FROM transactions
GROUP BY customer_id
HAVING SUM(amount) > 10000000;
```
### Câu 6
```sql
SELECT status, 
       COUNT(*) AS transaction_count, 
       SUM(amount) AS total_amount, 
       AVG(amount) AS avg_amount, 
       MIN(amount) AS min_amount, 
       MAX(amount) AS max_amount
FROM transactions
GROUP BY status;
```

## Ngày 4: JOIN
### Câu 1
```sql
SELECT c.customer_name, t.transaction_id, t.transaction_date, t.amount
FROM transactions AS t
JOIN customers AS c ON t.customer_id = c.customer_id;
```
### Câu 2
```sql
SELECT c.customer_id, c.customer_name, t.transaction_id, t.amount
FROM customers AS c
LEFT JOIN transactions AS t ON c.customer_id = t.customer_id;
```
### Câu 3
```sql
SELECT c.customer_id, c.customer_name
FROM customers AS c
LEFT JOIN transactions AS t ON c.customer_id = t.customer_id
WHERE t.transaction_id IS NULL;
```
### Câu 4
```sql
SELECT t.transaction_id, a.account_name, a.department, t.amount
FROM transactions AS t
JOIN accounts AS a ON t.account_id = a.account_id;
```
### Câu 5
```sql
SELECT a.department, SUM(t.amount) AS total_amount
FROM transactions AS t
JOIN accounts AS a ON t.account_id = a.account_id
GROUP BY a.department;
```
### Câu 6
```sql
SELECT t.transaction_id, t.customer_id, t.amount
FROM transactions AS t
LEFT JOIN customers AS c ON t.customer_id = c.customer_id
WHERE c.customer_id IS NULL;
```

## Ngày 5: Subquery và CTE
### Câu 1
```sql
SELECT *
FROM transactions
WHERE amount > (SELECT AVG(amount) FROM transactions);
```
### Câu 2
```sql
WITH customer_totals AS (
    SELECT customer_id, SUM(amount) AS total_amount
    FROM transactions
    GROUP BY customer_id
)
SELECT *
FROM customer_totals
WHERE total_amount > 10000000;
```
### Câu 3
```sql
SELECT *
FROM customers
WHERE customer_id IN (
    SELECT customer_id 
    FROM transactions 
    WHERE status = 'review'
);
```
### Câu 4
```sql
WITH monthly_sales AS (
    SELECT DATE_FORMAT(transaction_date, '%Y-%m') AS month,
           SUM(amount) AS total_amount
    FROM transactions
    GROUP BY DATE_FORMAT(transaction_date, '%Y-%m')
)
SELECT * FROM monthly_sales;
```
### Câu 5
```sql
WITH monthly_sales AS (
    SELECT DATE_FORMAT(transaction_date, '%Y-%m') AS month,
           SUM(amount) AS total_amount
    FROM transactions
    GROUP BY DATE_FORMAT(transaction_date, '%Y-%m')
)
SELECT * 
FROM monthly_sales
WHERE total_amount > 50000000;
```
### Câu 6
```sql
WITH customer_stats AS (
    SELECT customer_id, 
           SUM(amount) AS total_approved, 
           COUNT(*) AS approved_count
    FROM transactions
    WHERE status = 'approved'
    GROUP BY customer_id
)
SELECT * 
FROM customer_stats
WHERE approved_count >= 3;
```

## Ngày 6: Window functions
### Câu 1
```sql
SELECT customer_id, transaction_id, transaction_date, amount,
       ROW_NUMBER() OVER (PARTITION BY customer_id ORDER BY transaction_date ASC) AS rn
FROM transactions;
```
### Câu 2
```sql
SELECT customer_id, transaction_date, amount,
       SUM(amount) OVER (PARTITION BY customer_id ORDER BY transaction_date, transaction_id) AS running_total
FROM transactions;
```
### Câu 3
```sql
SELECT customer_id, transaction_id, amount,
       AVG(amount) OVER (PARTITION BY customer_id) AS avg_amount
FROM transactions;
```
### Câu 4
```sql
SELECT customer_id, transaction_id, amount,
       RANK() OVER (PARTITION BY customer_id ORDER BY amount DESC) AS amount_rank
FROM transactions;
```
### Câu 5
```sql
WITH transaction_avg AS (
    SELECT customer_id, transaction_id, amount,
           AVG(amount) OVER (PARTITION BY customer_id) AS avg_amount
    FROM transactions
)
SELECT * 
FROM transaction_avg
WHERE amount > 3 * avg_amount;
```
### Câu 6
```sql
WITH ranked_transactions AS (
    SELECT customer_id, transaction_id, transaction_date, amount,
           ROW_NUMBER() OVER (PARTITION BY customer_id ORDER BY transaction_date ASC, transaction_id ASC) AS rn
    FROM transactions
)
SELECT * 
FROM ranked_transactions
WHERE rn = 1;
```

## Ngày 7: Chất lượng dữ liệu và mini project
### Câu 1
```sql
SELECT status, COUNT(*) AS transaction_count
FROM transactions
GROUP BY status;
```
### Câu 2
```sql
SELECT *
FROM transactions
WHERE amount < 0;
```
### Câu 3
```sql
SELECT t.*
FROM transactions AS t
LEFT JOIN customers AS c ON t.customer_id = c.customer_id
WHERE c.customer_id IS NULL;
```
### Câu 4
```sql
SELECT DATE_FORMAT(transaction_date, '%Y-%m') AS month,
       SUM(amount) AS total_approved,
       COUNT(*) AS approved_count,
       AVG(amount) AS avg_approved_amount
FROM transactions
WHERE status = 'approved'
GROUP BY DATE_FORMAT(transaction_date, '%Y-%m');
```
### Câu 5
```sql
SELECT c.customer_id, c.customer_name, c.city, 
       SUM(t.amount) AS total_approved, 
       COUNT(t.transaction_id) AS total_transactions
FROM customers AS c
JOIN transactions AS t ON c.customer_id = t.customer_id
WHERE t.status = 'approved'
GROUP BY c.customer_id, c.customer_name, c.city
ORDER BY total_approved DESC
LIMIT 10;
```
### Câu 6
```sql
WITH approved_totals AS (
    SELECT customer_id, SUM(amount) AS total_approved
    FROM transactions
    WHERE status = 'approved'
    GROUP BY customer_id
    HAVING SUM(amount) > 10000000
)
SELECT c.*, a.total_approved
FROM customers AS c
JOIN approved_totals AS a ON c.customer_id = a.customer_id
WHERE c.customer_id IN (
    SELECT customer_id 
    FROM transactions 
    WHERE status = 'review'
);
```
### Câu 7
```sql
WITH daily_approved AS (
    SELECT transaction_date, SUM(amount) AS daily_total
    FROM transactions
    WHERE status = 'approved'
    GROUP BY transaction_date
)
SELECT transaction_date, daily_total,
       SUM(daily_total) OVER (ORDER BY transaction_date) AS running_total
FROM daily_approved
ORDER BY transaction_date;
```
### Câu 8
```sql
CREATE TABLE transactions_audit (
    audit_id INT AUTO_INCREMENT PRIMARY KEY,
    transaction_id INT,
    reason VARCHAR(255),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```
### Câu 9
```sql
INSERT INTO transactions_audit (transaction_id, reason)
SELECT transaction_id, 'Amount is negative'
FROM transactions
WHERE amount < 0;
```
### Câu 10
```sql
-- Kiểm tra trước khi cập nhật
SELECT *
FROM transactions
WHERE amount < 0;

-- Lệnh cập nhật
UPDATE transactions
SET status = 'review'
WHERE amount < 0;
```
