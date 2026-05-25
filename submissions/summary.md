# Test Summary — Báo cáo tổng hợp kiểm thử

> **Hướng dẫn**: Đây là hoạt động **Quality Assurance** — bạn đánh giá chất lượng tổng thể của phần mềm, không chỉ liệt kê lỗi.

---

## 1. Thông tin nhóm

| Mục | Thông tin |
|-----|----------|
| **Nhóm** | `Group 20` |
| **Lớp** | `ICT.1` |
| **Ngày báo cáo** | `25/05/2026` |
## 2. Tổng quan kết quả

| Chỉ số | Giá trị |
|--------|---------|
| Tổng số test case | 19 |
| Pass | 16 |
| Fail | 3 |
| Blocked | 0 |
| Not Run | 0 |
| **Tỷ lệ Pass** | 84.2% |
| **Số bug phát hiện** | 4 |

### Phân bổ theo nhóm chức năng

| Nhóm chức năng | TC | Pass | Fail | Bug | Đánh giá |
|---------------|-----|------|------|-----|---------|
| Login (REQ-01) | 5 | 5 | 0 | 0 | Hoạt động hoàn toàn ổn định và trả về đúng thông báo lỗi trong mọi kịch bản đầu vào. |
| View Book List (REQ-02) | 6 | 6 | 0 | 0 | Giao diện hiển thị trực quan, đồng bộ trạng thái sách thời gian thực chính xác sau khi mượn/trả. |
| Borrow Books (REQ-04) | 6 | 4 | 2 | 2 | Tồn tại lỗi logic nghiêm trọng cho phép mượn vượt giới hạn 3 sách và hiển thị sai thông báo lỗi cho TV tạm ngưng. |
| Return Books (REQ-05) | 2 | 1 | 1 | 1 | Trả sách hoạt động bình thường, nhưng khi trả quá hạn hệ thống hoàn toàn không hiển thị cảnh báo trễ hạn. |

### Phân bổ bug theo mức độ

| Mức độ | Số lượng | Bug IDs |
|--------|---------|---------|
| High | 1 | BUG-02 (Cho phép mượn sách thứ 4) |
| Medium | 3 | BUG-01 (Thủ thư thiếu nút mượn sách hộ), BUG-03 (Không hiện cảnh báo trả quá hạn), BUG-04 (Sai thông báo lỗi TV tạm ngưng) |
| Low | 0 | — |

---

## 3. Kỹ thuật thiết kế đã sử dụng

| Kỹ thuật | Áp dụng cho REQ nào? | Số TC sử dụng | Giải thích cách áp dụng |
|----------|---------------------|---------------|------------------------|
| EP (Equivalence Partitioning) | REQ-01, REQ-02, REQ-04, REQ-05 | 17 | Phân chia các phân vùng tương đương cho dữ liệu đầu vào hợp lệ/không hợp lệ (VD: trạng thái sách, vai trò tài khoản đăng nhập, trạng thái hoạt động của thành viên). |
| BVA (Boundary Value Analysis) | REQ-04, REQ-05 | 3 | Kiểm thử tại các giá trị biên quan trọng (VD: cố tình mượn cuốn sách thứ 4 khi đã chạm giới hạn 3 sách tại TC-17; biên thời gian trả sách đúng hạn vs trễ hạn tại TC-19). |

---

## 4. Phân tích chất lượng phần mềm

### 4.1. Điểm mạnh
- Giao diện thân thiện, dễ sử dụng, tốc độ phản hồi cực nhanh do dữ liệu lưu in-memory.
- Đồng bộ hóa trạng thái sách thời gian thực giữa tab **Sách** và tab **Mượn/Trả** mà không cần tải lại trang.
- Chức năng đăng nhập phân quyền rõ ràng giữa Thủ thư và Thành viên.

### 4.2. Điểm yếu
- Lỗi logic nghiêm trọng trong việc kiểm soát giới hạn mượn sách của Thành viên (BUG-02).
- Phản hồi thông tin lỗi bị sai lệch cho Thành viên bị tạm ngưng (BUG-04).
- Hệ thống hoàn toàn bỏ qua việc hiển thị cảnh báo trễ hạn khi Thành viên trả sách quá hạn (BUG-03).
- Sự không đồng nhất giữa SRS và UI khi vai trò Thủ thư hoàn toàn thiếu tính năng mượn sách hộ cho Thành viên khác (BUG-01).

---

## 5. Đề xuất ưu tiên sửa lỗi

| Thứ tự | Bug | Mức độ | Lý do ưu tiên |
|--------|-----|--------|---------------|
| 1 | BUG-02 (Cho mượn vượt giới hạn 3 sách) | High | Đây là lỗi logic kinh doanh nghiêm trọng nhất, làm thất thoát tài nguyên sách của thư viện và vi phạm trực tiếp quy tắc nghiệp vụ cốt lõi. |
| 2 | BUG-04 (Sai thông báo lỗi cho TV bị tạm ngưng) | Medium | Gây bối rối rất lớn cho người dùng và ảnh hưởng đến trải nghiệm dịch vụ hỗ trợ (tài khoản tạm ngưng lại báo hết hạn). |
| 3 | BUG-03 (Không hiển thị cảnh báo trả quá hạn) | Medium | Vi phạm quy tắc phản hồi nghiệp vụ của REQ-05 khi có thành viên trả sách quá hạn lâu ngày. |
| 4 | BUG-01 (Thủ thư thiếu nút mượn hộ) | Medium | Thiếu hụt một phần luồng quy trình làm việc chuẩn của Thủ thư được mô tả trong SRS, cần bổ sung giao diện. |

---

## 6. Kết luận

**Hệ thống CHƯA sẵn sàng phát hành (NOT READY FOR RELEASE)**. Mặc dù giao diện và luồng mượn/trả cơ bản chạy mượt mà, nhưng các lỗi logic kinh doanh cốt lõi (BUG-02) và lỗi thiếu/sai cảnh báo nghiệp vụ (BUG-03, BUG-04) là các rào cản lớn. Cần lập tức khắc phục BUG-02 và BUG-03 trước khi cho phép hệ thống triển khai thực tế.

---

## 7. Bài học rút ra (Tùy chọn)

`<!-- Nhóm bạn học được gì từ quá trình kiểm thử này? -->`

---

## 8. Khai báo sử dụng AI (Tùy chọn)

> Nếu nhóm có sử dụng công cụ AI (ChatGPT, Copilot, Gemini...), hãy ghi rõ bên dưới. Khai báo trung thực **không ảnh hưởng điểm** — đây là kỹ năng minh bạch trong nghề.

| Công cụ AI | Dùng cho phần nào | Bạn đã kiểm tra/chỉnh sửa thế nào |
|------------|-------------------|-----------------------------------|
| Claude | Doccuments | Analyze and summarize doccument, search for specific term in doccument faster than  |
