# Bug Reports — Báo cáo lỗi

> **Hướng dẫn**: Tạo 1 mục bug cho mỗi TC có kết quả **Fail**.
> Xem [examples/sample-bug-report.md](../examples/sample-bug-report.md) để hiểu cách viết bug report tốt.
> Mỗi bug cần: tiêu đề mô tả hành vi lỗi, bước tái hiện, expected vs actual, severity + giải thích.

| Thông tin | |
|---|---|
| **Nhóm** | `Group 20` |
| **Ngày báo cáo** | `25/05/2026` |

---

## BUG-01

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-01 |
| **TC liên quan** | `TC- (Nghiệp vụ mượn sách của Thủ thư)` |
| **REQ liên quan** | `REQ-04 & Overview` |
| **Mức độ** | `Medium` |
| **Người phát hiện** | `Đỗ Minh Tấn` |
| **Ngày phát hiện** | `25/05/2026` |
| **Trạng thái** | `Open` |

**Tiêu đề:**
Thủ thư không thể thực hiện thao tác mượn sách cho thành viên (thiếu chức năng tạo phiếu mượn trên giao diện của Thủ thư).

**Môi trường:**
- Trình duyệt: Chrome 148.0.7778.168
- Hệ điều hành: Windows
- Ngôn ngữ giao diện: Tiếng Việt

**Điều kiện tiên quyết:**
Đã đăng nhập tài khoản Thủ thư (`librarian@library.com`), dữ liệu hệ thống ở trạng thái ban đầu (seed data).

**Bước tái hiện:**
1. Truy cập trang web https://stqa.rbc.vn và đăng nhập tài khoản: `librarian@library.com` / `admin123`.
2. Quan sát tab **Sách**: Không có nút mượn sách (biểu tượng **+**) bên cạnh bất kỳ đầu sách nào ở trạng thái "Có sẵn".
3. Chuyển sang tab **Mượn / Trả**:
   - Chỉ hiển thị danh sách tìm kiếm phiếu mượn và nút **Trả sách** (Return) đối với các phiếu mượn đang hoạt động.
   - Hoàn toàn không có bất kỳ nút, biểu tượng, hay form nhập liệu nào để Thủ thư bắt đầu thao tác tạo phiếu mượn mới cho một mã thành viên cụ thể.

**Kết quả mong đợi:**
Theo đặc tả nghiệp vụ tại tài liệu **SRS - Mục 1 (Tổng quan hệ thống)**, Thủ thư có quyền **"mượn/trả sách cho thành viên"**. Hệ thống phải hiển thị chức năng/nút mượn sách hoặc cho phép Thủ thư nhập mã thành viên để tạo phiếu mượn sách mới cho thành viên đó.

**Kết quả thực tế:**
Giao diện của Thủ thư hoàn toàn thiếu tính năng hoặc nút bấm để thực hiện mượn sách cho thành viên. Thủ thư chỉ có thể thực hiện thao tác trả sách cho các phiếu đã có sẵn từ trước.

**Tác động:**
Thủ thư không thể mượn sách giúp thành viên khi thành viên yêu cầu trực tiếp tại quầy, vi phạm nghiêm trọng đặc tả yêu cầu nghiệp vụ cốt lõi tại Mục 1 của SRS.

**Minh chứng:**
*(Chưa đính kèm ảnh)*

**Đề xuất xử lý:**
Bổ sung một nút "Tạo phiếu mượn" hoặc biểu tượng mượn sách (**+**) trên giao diện của Thủ thư. Khi nhấn vào, hệ thống sẽ hiển thị một form hoặc hộp thoại (dialog) yêu cầu nhập **Mã thành viên (Member ID)** và tiến hành kiểm tra các ràng buộc nghiệp vụ (giới hạn số sách, trạng thái thành viên, trạng thái sách) trước khi tạo phiếu mượn mới.

---

## BUG-02

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-02 |
| **TC liên quan** | `TC-17` |
| **REQ liên quan** | `REQ-04` |
| **Mức độ** | `High` |
| **Người phát hiện** | `Đỗ Minh Tấn` |
| **Ngày phát hiện** | `25/05/2026` |
| **Trạng thái** | `Open` |

**Tiêu đề:**
Hệ thống cho phép thành viên mượn sách thứ 4, vượt quá giới hạn tối đa (3 sách) quy định tại REQ-04.

**Môi trường:**
- Trình duyệt: Chrome 148.0.7778.168
- Hệ điều hành: Windows
- Ngôn ngữ giao diện: Tiếng Việt

**Điều kiện tiên quyết:**
Tài khoản Thành viên đang mượn đủ 3 cuốn sách (ví dụ: `ba.nguyen@email.com` đang mượn BOOK001, BOOK002, BOOK004).

**Bước tái hiện:**
1. Đăng nhập bằng tài khoản thành viên đang giữ 3 sách (`ba.nguyen@email.com` / `password123`).
2. Tại tab **Sách**, tìm một cuốn sách đang ở trạng thái "Có sẵn" (ví dụ: `BOOK005 - Trí tuệ nhân tạo đại cương`).
3. Nhấn vào nút mượn sách (**+**) bên cạnh BOOK005.
4. Hộp thoại xác nhận mượn sách xuất hiện, nhấn **Mượn**.

**Kết quả mong đợi:**
Hệ thống từ chối mượn, hiển thị thông báo lỗi phù hợp: "Đã đạt giới hạn mượn tối đa (3 sách)." Sách BOOK005 vẫn giữ trạng thái "Có sẵn" và không tạo phiếu mượn mới.

**Kết quả thực tế:**
Thao tác mượn sách diễn ra thành công. Thông báo "Book borrowed successfully!" hiển thị, trạng thái BOOK005 đổi sang "Currently Borrowed", và hệ thống tự động tạo thêm phiếu mượn thứ 4 trong tab Borrow/Return.

**Tác động:**
Vi phạm nghiêm trọng quy tắc nghiệp vụ cốt lõi giới hạn 3 sách/thành viên. Thành viên có thể mượn vô hạn sách nếu có sẵn trong thư viện.

**Minh chứng:**
*(Chưa đính kèm ảnh)*

**Đề xuất xử lý:**
Trong logic backend (hàm `borrowBook` ở `library_service.dart`), kiểm tra lại điều kiện giới hạn mượn: đảm bảo dùng toán tử so sánh `>=` (lớn hơn hoặc bằng) thay vì `>` (lớn hơn): `if (currentBorrowCount >= maxBooksPerMember)`.

---

## BUG-04

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-04 |
| **TC liên quan** | `TC-15` |
| **REQ liên quan** | `REQ-04` |
| **Mức độ** | `Medium` |
| **Người phát hiện** | `Đỗ Minh Tấn` |
| **Ngày phát hiện** | `25/05/2026` |
| **Trạng thái** | `Open` |

**Tiêu đề:**
Hệ thống hiển thị sai thông báo lỗi khi Thành viên bị "Tạm ngưng" thực hiện mượn sách (hiển thị lỗi hết hạn tài khoản thay vì bị tạm ngưng).

**Môi trường:**
- Trình duyệt: Chrome 148.0.7778.168
- Hệ điều hành: Windows
- Ngôn ngữ giao diện: Tiếng Việt

**Điều kiện tiên quyết:**
Sử dụng tài khoản bị Tạm ngưng (`cu.le@email.com` / `password123`).

**Bước tái hiện:**
1. Đăng nhập tài khoản `cu.le@email.com` / `password123`.
2. Tại tab **Sách**, tìm sách có sẵn (ví dụ: `BOOK001`).
3. Nhấn nút mượn sách (**+**), sau đó nhấn **Mượn** trên hộp thoại xác nhận.

**Kết quả mong đợi:**
Nghiệp vụ mượn sách bị từ chối với thông báo lỗi đúng thực tế: "Thành viên đang bị tạm ngưng. Không thể mượn sách." (hoặc tương đương tiếng Anh "Member is suspended...").

**Kết quả thực tế:**
Giao diện hiển thị thông báo từ chối nhưng với nội dung: **"Thành viên đã hết hạn. Không thể mượn sách."** (Member is expired).

**Tác động:**
Vi phạm yêu cầu mô tả đúng lý do từ chối mượn trong đặc tả REQ-04. Gây bối rối cho người dùng khi tài khoản bị tạm ngưng nhầm tưởng tài khoản của mình đã hết hạn sử dụng.

**Minh chứng:**
*(Chưa đính kèm ảnh)*

**Đề xuất xử lý:**
Kiểm tra lại hàm `borrowBook()` ở backend. Đảm bảo luồng check điều kiện trạng thái thành viên kiểm tra chính xác `MemberStatus.suspended` và trả về đúng chuỗi thông báo lỗi dành riêng cho trạng thái tạm ngưng trước khi kiểm tra trạng thái hết hạn hoặc ngược lại.

---

## BUG-03

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-03 |
| **TC liên quan** | `TC-19` |
| **REQ liên quan** | `REQ-05` |
| **Mức độ** | `Medium` |
| **Người phát hiện** | `Đỗ Minh Tấn` |
| **Ngày phát hiện** | `25/05/2026` |
| **Trạng thái** | `Open` |

**Tiêu đề:**
Trả sách quá hạn thành công nhưng hệ thống không hiển thị bất kỳ cảnh báo quá hạn nào như đặc tả REQ-05.

**Môi trường:**
- Trình duyệt: Chrome 148.0.7778.168
- Hệ điều hành: Windows
- Ngôn ngữ giao diện: Tiếng Việt

**Điều kiện tiên quyết:**
Đăng nhập tài khoản thành viên `ba.nguyen@email.com` / `password123`. Tài khoản đang có phiếu mượn `BR001` đã quá hạn (Hạn trả: 15/09/2024).

**Bước tái hiện:**
1. Đăng nhập tài khoản `ba.nguyen@email.com` / `password123`.
2. Chuyển sang tab **Mượn / Trả**.
3. Tại mục "Phiếu mượn của tôi", tìm phiếu mượn mã `BR001` (Sách: *Kiểm thử phần mềm nhập môn*, Hạn trả: `15/09/2024`).
4. Nhấn vào nút **Trả sách** (màu xanh lá cây) bên cạnh phiếu mượn.

**Kết quả mong đợi:**
Trả sách thành công. Hệ thống phải hiển thị một thông báo hoặc hộp thoại **cảnh báo quá hạn** rõ ràng (ví dụ: thông báo trễ hạn phạt hoặc số ngày trễ hạn) theo quy định tại REQ-05.

**Kết quả thực tế:**
Sách được trả thành công và chuyển trạng thái thành "Đã trả" (Returned), nhưng hệ thống **hoàn toàn không hiển thị bất kỳ cảnh báo hay thông báo quá hạn nào** lên màn hình.

**Tác động:**
Vi phạm trực tiếp yêu cầu nghiệp vụ cốt lõi tại đặc tả REQ-05 (Trả sách). Hệ thống không thể nhắc nhở hoặc lưu ý thành viên/thủ thư về hành vi mượn sách quá hạn.

**Minh chứng:**
*(Chưa đính kèm ảnh)*

**Đề xuất xử lý:**
Trong logic xử lý trả sách tại backend/frontend, bổ sung kiểm tra điều kiện so sánh giữa ngày trả thực tế (`returnDate`) và ngày hết hạn (`dueDate`). Nếu `returnDate > dueDate`, hãy hiển thị một hộp thoại cảnh báo trễ hạn (Overdue Dialog Alert) trước hoặc cùng lúc với thông báo trả sách thành công.

---

<!-- Copy template BUG trên để thêm BUG-05, BUG-06, ... cho mỗi TC Fail -->
