# Hướng dẫn giảng dạy SQL 7 ngày (Dành cho người chưa có kinh nghiệm sư phạm)

Tài liệu này cung cấp các "mẹo sư phạm", cách dùng phép ẩn dụ (ví dụ từ Excel) và cấu trúc thời gian để bạn có thể giảng dạy SQL cho một người hoàn toàn mới trong 7 ngày một cách dễ hiểu nhất.

## Nguyên tắc chung khi dạy
1. **Liên hệ với Excel/Google Sheets:** Đa số người làm data/phân tích đều biết Excel. Hãy giải thích SQL thông qua lăng kính Excel.
2. **"Tưởng tượng dữ liệu" trước khi gõ code:** Luôn yêu cầu học viên nhắm mắt lại hoặc vẽ ra giấy xem kết quả đầu ra trông như thế nào trước khi viết câu lệnh `SELECT`.
3. **Mô hình "Tell - Show - Do - Review":** 
   - *Tell:* Giải thích khái niệm (5 phút).
   - *Show:* Code mẫu và chạy thử cho học viên xem (5 phút).
   - *Do:* Để học viên tự gõ lại và làm bài tập (10 phút).
   - *Review:* Chữa bài và giải thích lỗi sai (5 phút).
4. **Không dạy thừa:** Chỉ tập trung vào các lệnh dùng để đi làm (SELECT, JOIN, GROUP BY). Tạm bỏ qua tối ưu hóa sâu hoặc thiết kế database phức tạp ở giai đoạn này.

---

## Ngày 1: SELECT, WHERE, ORDER BY, LIMIT
**Mục tiêu:** Giúp học viên không sợ SQL. Hiểu rằng SQL chỉ là cách "ra lệnh" cho máy tính đọc dữ liệu.

* **Ẩn dụ (Analogy):** 
  - Database = Tủ hồ sơ.
  - Table = Một quyển sổ / File Excel.
  - Column = Tiêu đề cột.
  - Row = Một dòng dữ liệu.
* **Cách dạy:**
  1. Mở Excel, cho xem một bảng dữ liệu mẫu. Hỏi: "Nếu em muốn lấy các khách hàng ở Hà Nội, em làm gì?". (Học viên: Filter cột City). -> "Trong SQL, cái phễu lọc đó gọi là `WHERE`."
  2. Dạy theo thứ tự suy nghĩ tự nhiên, không phải thứ tự gõ:
     - Tủ nào? (`FROM`)
     - Lọc điều kiện gì? (`WHERE`)
     - Lấy cột nào? (`SELECT`)
     - Sắp xếp ra sao? (`ORDER BY`)
* **Thực hành vẽ:** Vẽ lên giấy 3 cột (ID, Name, Age). Gạch chéo bỏ cột Age đi để minh họa cho lệnh `SELECT ID, Name`.

## Ngày 2: Điều kiện lọc, NULL và kiểu dữ liệu
**Mục tiêu:** Cẩn thận với các "cạm bẫy" khi lọc dữ liệu (Ngày tháng và NULL).

* **Ẩn dụ (Analogy):** 
  - `NULL` không phải là số không (0), cũng không phải khoảng trắng (" "). `NULL` là một ô Excel bạn chưa từng gõ gì vào (trống rỗng).
* **Cách dạy:**
  1. **Kiểu dữ liệu:** Đừng đi sâu vào `VARCHAR(255)` vs `CHAR`. Chỉ cần nói: "Số là số, Chữ là chữ (phải có ngoặc kép `' '`), Ngày tháng là ngày tháng".
  2. **Vấn đề lọc ngày tháng:** Hãy vẽ một trục thời gian. Nhấn mạnh việc `2026-01-31` thực chất hệ thống có thể hiểu là `2026-01-31 00:00:00`. Vì vậy dùng `>= 2026-01-01` và `< 2026-02-01` là cách an toàn nhất để ôm trọn tháng 1.
  3. **COALESCE:** Dạy cách dùng hàm này như hàm `IFERROR` hoặc thay thế giá trị trống trong Excel.

## Ngày 3: GROUP BY và hàm tổng hợp
**Mục tiêu:** Tư duy tổng hợp dữ liệu, bước đệm để làm báo cáo.

* **Ẩn dụ (Analogy):** `GROUP BY` chính là `Pivot Table` trong Excel.
  - Vùng "Rows" trong Pivot Table chính là các cột trong `GROUP BY`.
  - Vùng "Values" trong Pivot Table chính là `SUM()`, `COUNT()`, `AVG()`.
* **Cách dạy:**
  1. Yêu cầu học viên tưởng tượng có 10 tờ tiền các loại (10k, 20k, 50k) vứt trên bàn. 
  2. B1: Chia thành các cọc tiền giống nhau (`GROUP BY mệnh_giá`).
  3. B2: Đếm xem mỗi cọc có bao nhiêu tờ (`COUNT()`) hoặc tổng tiền mỗi cọc là bao nhiêu (`SUM()`).
  4. Trực quan hóa lỗi lớn nhất: Quên đưa cột báo cáo vào nhóm `GROUP BY`. "Em không thể báo cáo theo phòng ban nếu em không gom nhóm theo phòng ban".
  5. Phân biệt `WHERE` (lọc trước khi chia cọc) và `HAVING` (chia cọc xong, tính tổng rồi mới vứt các cọc nhỏ đi).

## Ngày 4: JOIN
**Mục tiêu:** Hiểu sức mạnh thực sự của CSDL Quan Hệ.

* **Ẩn dụ (Analogy):** `JOIN` chính là hàm `VLOOKUP` siêu cấp.
* **Cách dạy:**
  1. **Tại sao phải tách bảng?** Hỏi: "Nếu công ty có 1 triệu giao dịch, mà dòng nào cũng ghi lại tên, sđt, địa chỉ khách hàng thì chuyện gì xảy ra?" -> Tốn dung lượng, sửa địa chỉ rất cực. -> Tách ra.
  2. **Cách vẽ:** Hãy bắt học viên vẽ biểu đồ Venn (2 vòng tròn giao nhau).
     - Giao nhau (phần giữa) là `INNER JOIN`.
     - Lấy cả vòng trái là `LEFT JOIN`.
  3. Dạy kỹ về "Hiệu ứng nhân bản dòng" (Row Duplication): Lấy một ví dụ bảng A có 1 dòng, bảng B có 2 dòng trùng ID. Nối lại thành mấy dòng? (Thành 2). Từ đó nhắc học viên luôn dùng `COUNT(*)` trước và sau khi JOIN.

## Ngày 5: Subquery và CTE (WITH)
**Mục tiêu:** Viết code sạch, chia bài toán lớn thành các bài toán nhỏ.

* **Ẩn dụ (Analogy):** CTE giống như tạo một "Sheet nháp" (hoặc bảng phụ) trong Excel để tính toán trung gian trước khi copy kết quả sang Sheet Báo Cáo chính.
* **Cách dạy:**
  1. Đưa ra một bài toán dài (VD: Lấy KH có tổng chi tiêu > 10tr và thuộc Hà Nội). 
  2. Cho họ thấy nếu viết 1 lèo sẽ rất rối.
  3. Hướng dẫn viết CTE: 
     - Bước 1: Gom bảng tính tổng chi tiêu trước -> Gói lại đặt tên là `chi_tieu_KH`.
     - Bước 2: Nối bảng `chi_tieu_KH` với bảng `customers` để lấy thành phố Hà Nội và lọc > 10tr.
  4. Chỉ ra CTE giúp code dễ debug: Lỗi ở đâu thì chạy riêng khối CTE đó.

## Ngày 6: Window functions
**Mục tiêu:** Mở khóa tư duy phân tích nâng cao (Analytics).

* **Ẩn dụ (Analogy):** `GROUP BY` gom nhiều dòng thành 1 dòng. `Window Function` vẫn giữ nguyên các dòng, nhưng lén "nhìn" sang các dòng khác để tính toán (như tạo một cột mới trong Excel chứa tổng mà không bị gộp dòng).
* **Cách dạy:**
  1. Phân biệt rõ `GROUP BY` và `Window Function` (vẽ bảng minh họa Before - After).
  2. Dạy cấu trúc 3 phần rõ ràng:
     - `Hàm gì?` (Ví dụ: `ROW_NUMBER()`)
     - `OVER` (bắt đầu mở cửa sổ)
     - `PARTITION BY` (chia nhóm như thế nào) + `ORDER BY` (xếp hàng ra sao trong nhóm đó).
  3. Thực hành xếp hàng: "Giả sử cả lớp đứng thành từng hàng theo Quê Quán (Partition), rồi xếp theo Chiều cao (Order By). Row_Number sẽ đánh số 1, 2, 3... cho từng bạn trong từng hàng".

## Ngày 7: Chất lượng dữ liệu & Mini Project
**Mục tiêu:** Củng cố tư duy người làm Dữ Liệu (Data mindset): Dữ liệu không bao giờ hoàn hảo.

* **Cách dạy:**
  1. **Mindset:** Dạy học viên thói quen: Khi nhận 1 bảng mới, khoan lấy data ngay. Hãy đếm số dòng, check NULL cột khóa, check Min/Max xem có số âm hay số vô lý không.
  2. **DML (INSERT/UPDATE/DELETE):** Dạy rất lướt phần này để họ biết cú pháp, nhưng nhấn mạnh quy tắc vàng: **Luôn viết SELECT trước khi UPDATE/DELETE** để xem mình chuẩn bị xóa nhầm dữ liệu của ai không.
  3. **Mini Project:** Để học viên tự làm 100%, đóng vai người quản lý đòi báo cáo. Bắt họ phải comment code và giải thích tại sao lại dùng LEFT JOIN thay vì INNER JOIN.
