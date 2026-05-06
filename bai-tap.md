# Bài tập SQL MySQL trong 7 ngày

Hướng dẫn:

- Điền câu trả lời SQL vào phần `Đáp án của tôi`.
- Nếu chưa chắc, vẫn viết cách nghĩ của bạn. Khi kiểm tra, tôi sẽ chỉ ra lỗi cú pháp, lỗi logic và cách viết tốt hơn.
- Không cần xóa phần `Nhận xét của ChatGPT`; phần đó để tôi điền khi bạn yêu cầu kiểm tra.
- Các bài tập dùng bộ bảng giả định bên dưới. Bạn có thể tạo bảng thật trong MySQL hoặc chỉ viết truy vấn.

## Bộ bảng giả định

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

Lấy tất cả cột trong bảng `customers`.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

### Câu 2

Lấy các cột `customer_id`, `customer_name`, `city` trong bảng `customers`.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

### Câu 3

Lấy 10 giao dịch đầu tiên trong bảng `transactions`.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

### Câu 4

Lấy các giao dịch có `amount` lớn hơn 1000000.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

### Câu 5

Lấy các giao dịch có `status` là `approved`, sắp xếp theo `amount` giảm dần.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

### Câu 6

Lấy `transaction_id`, `customer_id`, `amount` của 5 giao dịch có số tiền cao nhất.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

---

## Ngày 2: Điều kiện lọc, NULL và kiểu dữ liệu

### Câu 1

Lấy các giao dịch trong tháng 1 năm 2026. Hãy viết theo cách an toàn cho cả cột `DATE` và `DATETIME`.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

### Câu 2

Lấy các giao dịch có `status` là `pending` hoặc `review`.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

### Câu 3

Lấy các khách hàng có tên bắt đầu bằng `Nguyễn`.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

### Câu 4

Tìm các giao dịch có `amount` bị thiếu.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

### Câu 5

Viết truy vấn lấy `transaction_id`, `amount`, và một cột mới tên `amount_clean`, trong đó nếu `amount` bị `NULL` thì thay bằng 0.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

### Câu 6

Tìm các giao dịch có `amount` âm hoặc bằng 0, vì đây là nhóm cần kiểm tra trong dữ liệu tài chính.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

---

## Ngày 3: GROUP BY và hàm tổng hợp

### Câu 1

Đếm tổng số giao dịch trong bảng `transactions`.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

### Câu 2

Tính tổng `amount` của tất cả giao dịch `approved`.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

### Câu 3

Tính số giao dịch và tổng tiền theo từng `customer_id`.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

### Câu 4

Tính tổng tiền theo từng ngày giao dịch.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

### Câu 5

Tìm các `customer_id` có tổng `amount` lớn hơn 10000000.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

### Câu 6

Tính số giao dịch, tổng tiền, trung bình, nhỏ nhất và lớn nhất của `amount` theo từng `status`.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

---

## Ngày 4: JOIN

### Câu 1

Nối bảng `customers` và `transactions` để lấy `customer_name`, `transaction_id`, `transaction_date`, `amount`.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

### Câu 2

Lấy danh sách tất cả khách hàng và giao dịch của họ nếu có. Khách hàng không có giao dịch vẫn phải xuất hiện.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

### Câu 3

Tìm các khách hàng chưa có giao dịch nào.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

### Câu 4

Nối `transactions` với `accounts` để lấy tên tài khoản và phòng ban của mỗi giao dịch.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

### Câu 5

Tính tổng `amount` theo từng `department`.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

### Câu 6

Tìm các giao dịch không có `customer_id` hợp lệ trong bảng `customers`.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

---

## Ngày 5: Subquery và CTE

### Câu 1

Lấy các giao dịch có `amount` lớn hơn giá trị trung bình của tất cả giao dịch.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

### Câu 2

Dùng CTE để tính tổng tiền theo khách hàng, sau đó lấy các khách hàng có tổng tiền lớn hơn 10000000.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

### Câu 3

Dùng subquery để lấy danh sách khách hàng có ít nhất một giao dịch `review`.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

### Câu 4

Dùng CTE để tính tổng tiền theo tháng. Cột tháng đặt tên là `month`, định dạng `YYYY-MM`.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

### Câu 5

Từ CTE tổng tiền theo tháng, lấy các tháng có tổng tiền lớn hơn 50000000.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

### Câu 6

Dùng CTE để tạo báo cáo gồm `customer_id`, tổng tiền `approved`, số giao dịch `approved`, rồi chỉ lấy khách hàng có ít nhất 3 giao dịch `approved`.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

---

## Ngày 6: Window functions

### Câu 1

Dùng `ROW_NUMBER()` để đánh số thứ tự giao dịch của mỗi khách hàng theo `transaction_date` tăng dần.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

### Câu 2

Tính tổng lũy kế `amount` theo từng khách hàng, sắp xếp theo ngày giao dịch.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

### Câu 3

Tính trung bình `amount` của từng khách hàng và hiển thị trên mỗi dòng giao dịch.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

### Câu 4

Xếp hạng giao dịch theo `amount` giảm dần trong từng khách hàng bằng `RANK()`.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

### Câu 5

Tìm các giao dịch có `amount` lớn hơn 3 lần trung bình `amount` của chính khách hàng đó.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

### Câu 6

Tìm giao dịch đầu tiên của mỗi khách hàng theo `transaction_date`. Nếu trùng ngày, dùng `transaction_id` để ổn định thứ tự.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

---

## Ngày 7: Chất lượng dữ liệu và mini project

### Câu 1

Đếm số giao dịch theo từng `status`.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

### Câu 2

Tìm các giao dịch có `amount` âm.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

### Câu 3

Tìm các giao dịch không có `customer_id` hợp lệ trong bảng `customers`.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

### Câu 4

Viết truy vấn báo cáo gồm: `month`, tổng doanh thu approved, số giao dịch approved, giá trị trung bình mỗi giao dịch approved.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

### Câu 5

Viết truy vấn mini project: top 10 khách hàng có tổng `amount` approved cao nhất, kèm tên khách hàng, thành phố, tổng tiền và số giao dịch.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

### Câu 6

Viết truy vấn tìm các khách hàng có tổng `amount` approved lớn hơn 10000000 nhưng vẫn có ít nhất một giao dịch `review`.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

### Câu 7

Viết truy vấn tổng lũy kế doanh thu `approved` theo ngày trên toàn bộ hệ thống.

Đáp án của tôi:

```sql

```

Nhận xét của ChatGPT:

```text

```

---

## Prompt để kiểm tra đáp án

Sau khi điền xong, gửi tôi prompt này:

```text
Hãy check đáp án SQL trong file bai_tap_sql_mysql_7_ngay.md.
Với mỗi câu, nếu đúng thì ghi "Đúng" vào phần Nhận xét của ChatGPT.
Nếu sai, ghi lỗi sai, đáp án đúng, và giải thích ngắn gọn.
Không xóa đáp án của tôi.
```

