# Test Cases — Bảng trường hợp kiểm thử

> **Hướng dẫn**: Viết tối thiểu **20 TC** phủ đủ các chức năng chính (REQ-01 → REQ-08).
> Xem [examples/sample-test-case.md](../examples/sample-test-case.md) để hiểu cách viết TC tốt.
> Tự tổ chức và phân nhóm test case theo cách hợp lý nhất.

| Thông tin | |
|---|---|
| **Nhóm** | `<!-- Tên nhóm -->` |
| **Ngày tạo** | `<!-- DD/MM/YYYY -->` |
| **Hệ thống** | https://stqa.rbc.vn |
| **Tham chiếu** | SRS v1.0 |

---

## Bước 1: Mô hình hóa miền đầu vào — Input Domain Modeling (IDM)

> 📖 **Textbook:** Chương 6 — *Input Domain Modeling*, Paul Ammann & Jeff Offutt.
>
> **Trước khi viết Test Case**, nhóm **phải** phân tích miền đầu vào bằng bảng IDM bên dưới.
> Mỗi chức năng cần xác định: **Đặc tính (Characteristic)**, **Phân vùng (Block/Partition)**, và **Giá trị đại diện (Value)**.

### IDM — Đăng nhập (REQ-01)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Email có tồn tại trong DB? | Có | `librarian@library.com` | Đăng nhập thành công |
| | Không | `noone@email.com` | Thông báo lỗi |
| Mật khẩu có đúng? | Đúng | `admin123` | Đăng nhập thành công |
| | Sai | `wrongpass` | Thông báo lỗi |
| Ô nhập có rỗng? | Không rỗng | (giá trị bất kỳ) | Xử lý bình thường |
| | Rỗng | `""` | Thông báo "Vui lòng nhập..." |

### IDM — Xem danh sách sách (REQ-02)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Vai trò người dùng? | Thủ thư | LIB001 | Xem được toàn bộ danh sách sách |
| | Thành viên | MEM002 | Xem được toàn bộ danh sách sách |
| Trạng thái sách hiển thị? | Có sẵn | BOOK001 | Hiển thị "Có sẵn" |
| | Đang mượn | BOOK003 | Hiển thị "Đang mượn" |
| | Thất lạc | BOOK007 | Hiển thị "Thất lạc" |
| Thông tin mỗi sách? | Đầy đủ 5 trường | (bất kỳ sách nào) | Hiển thị: tên, tác giả, thể loại, năm XB, trạng thái |
| Cập nhật real-time? | Sau mượn | BOOK001 vừa được mượn | Trạng thái ngay lập tức → "Đang mượn" (không cần refresh) |
| | Sau trả | BOOK003 vừa được trả | Trạng thái ngay lập tức → "Có sẵn" (không cần refresh) |

### IDM — Tìm kiếm sách (REQ-03)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Từ khóa có tồn tại trong DB? | Có (tên sách) | `"Flutter"` | Hiển thị sách chứa "Flutter" |
| | Có (tên tác giả) | `"Nguyễn"` | Hiển thị sách của tác giả Nguyễn |
| | Không | `"XYZ123"` | Danh sách rỗng |
| Phân biệt HOA/thường? | Chữ thường | `"flutter"` | Kết quả giống "Flutter" |
| | Chữ HOA | `"FLUTTER"` | Kết quả giống "Flutter" |

### IDM — Mượn sách (REQ-04, REQ-05)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Trạng thái sách? | Có sẵn | BOOK001 | Cho phép mượn |
| | Đang mượn | BOOK003 | Không cho phép |
| | Thất lạc | BOOK007 | Không cho phép |
| Trạng thái thành viên? | Hoạt động | MEM002 | Cho phép mượn |
| | Tạm ngưng | MEM004 | Từ chối, thông báo lỗi |
| | Hết hạn | MEM005 | Từ chối, thông báo lỗi |
| Số sách đang mượn? | < 3 (BVA: 0, 1, 2) | MEM006 (0 sách) | Cho phép mượn |
| | = 3 (BVA: giới hạn) | MEM đã mượn 3 sách | Từ chối, thông báo vượt giới hạn |

### IDM — `<!-- Nhóm tự bổ sung cho REQ-05 đến REQ-08 -->`

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| `<!-- Nhóm tự điền -->` | | | |

> 💡 **Gợi ý kỹ thuật**: Sử dụng **Phân lớp tương đương (EP)** cho các phân vùng rời rạc, **Phân tích giá trị biên (BVA)** cho các phân vùng số (ví dụ: giới hạn 3 sách). Xem textbook §6.1–6.3.

---

## Bước 2: Test Cases

<!-- Tự tổ chức bảng test case: có thể chia nhóm theo chức năng, theo REQ, hoặc theo luồng nghiệp vụ — tùy nhóm quyết định. -->
<!-- Mỗi TC phải ánh xạ ngược về ít nhất 1 dòng trong bảng IDM ở Bước 1. -->

| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC-01 | Đăng nhập thành công — tài khoản Thủ thư | Trang đăng nhập đang hiển thị, chưa đăng nhập | 1. Nhập email vào ô **Email**. 2. Nhập mật khẩu vào ô **Mật khẩu**. 3. Nhấn nút **Đăng nhập**. | Email: `librarian@library.com` / Mật khẩu: `admin123` | Chuyển sang trang chủ. Hệ thống nhận diện đúng vai trò Thủ thư: hiển thị tên + "(Thủ thư)", truy cập được cả 3 chức năng: Sách, Mượn / Trả, Thành viên. | REQ-01 | EP |
| TC-02 | Đăng nhập thành công — tài khoản Thành viên | Trang đăng nhập đang hiển thị, chưa đăng nhập | 1. Nhập email vào ô **Email**. 2. Nhập mật khẩu vào ô **Mật khẩu**. 3. Nhấn nút **Đăng nhập**. | Email: `ba.nguyen@email.com` / Mật khẩu: `password123` | Chuyển sang trang chủ. Hệ thống nhận diện đúng vai trò Thành viên: hiển thị tên + "(Thành viên)", **không** truy cập được chức năng Thành viên (chỉ Thủ thư mới có). | REQ-01 | EP |
| TC-03 | Đăng nhập với email không tồn tại trong hệ thống | Trang đăng nhập đang hiển thị, chưa đăng nhập | 1. Nhập email không tồn tại vào ô **Email**. 2. Nhập mật khẩu bất kỳ vào ô **Mật khẩu**. 3. Nhấn nút **Đăng nhập**. | Email: `randomuser@gmail.com` / Mật khẩu: `qweqweqwe` | Đăng nhập thất bại, ở lại trang đăng nhập. Thông báo lỗi: **"Không tìm thấy thành viên."** | REQ-01 | EP |
| TC-04 | Đăng nhập với mật khẩu sai (email đúng) | Trang đăng nhập đang hiển thị, chưa đăng nhập | 1. Nhập email hợp lệ vào ô **Email**. 2. Nhập mật khẩu **sai** vào ô **Mật khẩu**. 3. Nhấn nút **Đăng nhập**. | Email: `librarian@library.com` / Mật khẩu: `qweqweqwe` | Đăng nhập thất bại, ở lại trang đăng nhập. Thông báo lỗi: **"Mật khẩu không đúng."** — khác biệt với thông báo email sai. | REQ-01 | EP |
| TC-05 | Đăng nhập khi để trống cả hai ô | Trang đăng nhập đang hiển thị, chưa đăng nhập | 1. Để trống ô **Email**. 2. Để trống ô **Mật khẩu**. 3. Nhấn nút **Đăng nhập**. | Email: *(trống)* / Mật khẩu: *(trống)* | Đăng nhập thất bại, ở lại trang đăng nhập. Thông báo lỗi: **"Vui lòng nhập email và mật khẩu."** | REQ-01 | EP |
| TC-06 | Thủ thư xem danh sách sách — hiển thị đầy đủ 20 sách và đủ thông tin mỗi sách | Đã đăng nhập tài khoản Thủ thư, đang ở tab **Sách** | 1. Quan sát danh sách sách trên màn hình. 2. Đếm số lượng sách hiển thị. 3. Kiểm tra thông tin của một sách bất kỳ (ví dụ: BOOK001). | Tài khoản: `librarian@library.com` / `admin123` | Danh sách hiển thị đủ **20 sách**. Mỗi sách có đầy đủ 5 trường: **tên sách**, **tác giả**, **thể loại**, **năm xuất bản**, **trạng thái**. | REQ-02 | EP |
| TC-07 | Thành viên xem danh sách sách — hiển thị đầy đủ 20 sách và đủ thông tin mỗi sách | Đã đăng nhập tài khoản Thành viên, đang ở tab **Sách** | 1. Quan sát danh sách sách trên màn hình. 2. Đếm số lượng sách hiển thị. 3. Kiểm tra thông tin của một sách bất kỳ (ví dụ: BOOK001). | Tài khoản: `ba.nguyen@email.com` / `password123` | Danh sách hiển thị đủ **20 sách**. Mỗi sách có đầy đủ 5 trường: **tên sách**, **tác giả**, **thể loại**, **năm xuất bản**, **trạng thái**. | REQ-02 | EP |
| TC-08 | Sách có trạng thái "Có sẵn" hiển thị đúng trạng thái | Đã đăng nhập (bất kỳ vai trò), đang ở tab **Sách**, dữ liệu ở trạng thái ban đầu (seed data) | 1. Tìm **BOOK001** (Lập trình Flutter cơ bản) trong danh sách. 2. Đọc trạng thái hiển thị của sách này. | Sách: BOOK001 — trạng thái ban đầu theo seed data là **Có sẵn** | Trạng thái của BOOK001 hiển thị là **"Có sẵn"**. | REQ-02 | EP |
| TC-09 | Sách đang được mượn hiển thị đúng trạng thái "Đang mượn" | Đã đăng nhập (bất kỳ vai trò), đang ở tab **Sách**, dữ liệu ở trạng thái ban đầu (seed data) | 1. Tìm **BOOK003** (Kiểm thử phần mềm nhập môn) trong danh sách. 2. Đọc trạng thái hiển thị của sách này. | Sách: BOOK003 — trạng thái ban đầu theo seed data là đang được mượn bởi MEM002 | Trạng thái của BOOK003 hiển thị là **"Đang mượn"**. | REQ-02 | EP |
| TC-10 | Trạng thái sách cập nhật real-time ngay sau khi Thành viên mượn — không cần refresh | Đã đăng nhập tài khoản Thành viên (MEM002), đang ở tab **Sách**, BOOK001 đang ở trạng thái "Có sẵn" | 1. Xác nhận BOOK001 hiển thị trạng thái **"Có sẵn"**. 2. Nhấn nút **+** bên cạnh BOOK001. 3. Dialog xác nhận xuất hiện — nhấn **Mượn**. 4. Quan sát trạng thái BOOK001 ngay sau đó mà không tải lại trang. | Sách: BOOK001 / Tài khoản: `ba.nguyen@email.com` / `password123` | Dialog xác nhận: "Bạn muốn mượn 'Lập trình Flutter cơ bản'?". Sau khi xác nhận: trạng thái BOOK001 **chuyển thành "Đang mượn" ngay lập tức**, thông báo **"Mượn sách thành công!"** xuất hiện. | REQ-02 | EP |
| TC-11 | Trạng thái sách cập nhật real-time ngay sau khi Thủ thư trả — không cần refresh | Đã đăng nhập tài khoản Thủ thư, dữ liệu ban đầu: BOOK003 đang ở trạng thái "Đang mượn" (phiếu BR001 của MEM002) | 1. Ở tab **Sách**: xác nhận BOOK003 hiển thị **"Đang mượn"**. 2. Chuyển sang tab **Mượn / Trả**. 3. Tìm phiếu BR001 (Kiểm thử phần mềm nhập môn — Đang mượn), nhấn nút **Trả sách**. 4. Chuyển lại tab **Sách**, quan sát trạng thái BOOK003. | Phiếu mượn: BR001 / Sách: BOOK003 | BR001 chuyển sang trạng thái **"Đã trả"** với ngày trả ghi nhận. Thông báo **"Trả sách thành công."** xuất hiện. Tại tab Sách: BOOK003 **chuyển thành "Có sẵn" ngay lập tức** mà không cần tải lại trang. | REQ-02 | EP |

---

## Tổng hợp

| Nhóm chức năng | Số TC | REQ phủ | Kỹ thuật IDM áp dụng |
|----------------|-------|---------|----------------------|
| Đăng nhập | 5 | REQ-01 | EP |
| Xem danh sách sách | 6 | REQ-02 | EP |
| **Tổng** | **11** | REQ-01, REQ-02 | EP |
