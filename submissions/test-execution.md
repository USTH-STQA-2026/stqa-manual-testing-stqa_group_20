# Test Execution — Kết quả thực thi kiểm thử

> **Hướng dẫn**: Chạy từng TC trên hệ thống https://stqa.rbc.vn, ghi lại kết quả thực tế.
> Kết luận: **Pass** (kết quả đúng), **Fail** (kết quả sai → tạo bug report), **Blocked** (không thực hiện được vì lỗi khác chặn), **Not Run** (chưa chạy).

| Thông tin | |
|---|---|
| **Nhóm** | `Nhóm 20` |
| **Ngày thực thi** | 13/05/2026 |
| **Trình duyệt** | Chrome 148.0.7778.168  |
| **Hệ điều hành** | Windows |

---

## Kết quả chi tiết

| Mã TC | Nhóm chức năng | Kết quả mong đợi (tóm tắt) | Kết quả thực tế | Kết luận | Minh chứng | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|-----|
| TC-01 | Đăng nhập | Chuyển trang chủ, hiển thị tên + "(Thủ thư)", thấy 3 tab | Chuyển trang chủ. AppBar hiển thị "Nguyễn Thủ Thư (Thủ thư)". Hiển thị đủ 3 tab: Sách, Mượn / Trả, Thành viên. | **Pass** | [TC-01_librarian_login.png](../screenshots/TC-01_librarian_login.png) | — |
| TC-02 | Đăng nhập | Chuyển trang chủ, hiển thị tên + "(Thành viên)", không thấy tab Thành viên | Chuyển trang chủ. AppBar hiển thị "Nguyễn Học Bá (Thành viên)". Chỉ có 2 tab: Sách, Mượn / Trả — không có tab Thành viên. | **Pass** | [TC-02_member_login.png](../screenshots/TC-02_member_login.png) | — |
| TC-03 | Đăng nhập | Đăng nhập thất bại, thông báo "Không tìm thấy thành viên." | Ở lại trang đăng nhập. Thông báo lỗi xuất hiện: **"Không tìm thấy thành viên."** | **Pass** | [TC-03_email_not_found.png](../screenshots/TC-03_email_not_found.png) | — |
| TC-04 | Đăng nhập | Đăng nhập thất bại, thông báo "Mật khẩu không đúng." | Ở lại trang đăng nhập. Thông báo lỗi xuất hiện: **"Mật khẩu không đúng."** (khác với thông báo email sai). | **Pass** | [TC-04_wrong_password.png](../screenshots/TC-04_wrong_password.png) | — |
| TC-05 | Đăng nhập | Đăng nhập thất bại, thông báo "Vui lòng nhập email và mật khẩu." | Ở lại trang đăng nhập. Thông báo lỗi xuất hiện: **"Vui lòng nhập email và mật khẩu."** | **Pass** | [TC-05_empty_fields.png](../screenshots/TC-05_empty_fields.png) | — |
| TC-06 | Xem danh sách sách | Thủ thư thấy đủ 20 sách, mỗi sách có 5 trường thông tin | Hiển thị đủ **20/20 sách** khi cuộn danh sách (BOOK001–BOOK020). Mỗi sách có: tên sách, tác giả, thể loại, năm xuất bản, trạng thái. | **Pass** | [TC-06a (đầu danh sách)](../screenshots/TC-06a_librarian_book_list_top.png) · [TC-06b (cuối danh sách)](../screenshots/TC-06b_librarian_book_list_bottom.png) | — |
| TC-07 | Xem danh sách sách | Thành viên thấy đủ 20 sách, mỗi sách có 5 trường thông tin | Hiển thị đủ **20/20 sách** khi cuộn danh sách. Sách có sẵn có thêm nút **+** (mượn); sách đang mượn chỉ hiển thị nhãn trạng thái. | **Pass** | [TC-07a (đầu danh sách)](../screenshots/TC-07a_member_book_list_top.png) · [TC-07b (cuối danh sách)](../screenshots/TC-07b_member_book_list_bottom.png) | — |
| TC-08 | Xem danh sách sách | BOOK001 hiển thị trạng thái "Có sẵn" | BOOK001 (Lập trình Flutter cơ bản) hiển thị nhãn trạng thái: **"Có sẵn"**. | **Pass** | [TC-08_book001_co_san.png](../screenshots/TC-08_book001_co_san.png) | — |
| TC-09 | Xem danh sách sách | BOOK003 hiển thị trạng thái "Đang mượn" | BOOK003 (Kiểm thử phần mềm nhập môn) hiển thị nhãn trạng thái: **"Đang mượn"**. | **Pass** | [TC-09_book003_dang_muon.png](../screenshots/TC-09_book003_dang_muon.png) | — |
| TC-10 | Xem danh sách sách | Sau khi mượn: BOOK001 chuyển thành "Đang mượn" ngay, không cần refresh | Click **+** → Dialog: "Bạn muốn mượn 'Lập trình Flutter cơ bản'?" → Click **Mượn**. BOOK001 chuyển thành **"Đang mượn"** ngay lập tức. Thông báo **"Mượn sách thành công!"** xuất hiện. | **Pass** | [TC-10a (trước)](../screenshots/TC-10a_before_borrow.png) · [TC-10b (dialog)](../screenshots/TC-10b_confirm_dialog.png) · [TC-10c (sau)](../screenshots/TC-10c_after_borrow.png) | — |
| TC-11 | Xem danh sách sách | Sau khi trả: BOOK003 chuyển thành "Có sẵn" ngay, không cần refresh | Tab Mượn/Trả → Click **Trả sách** trên BR001 → Thông báo **"Trả sách thành công."**, BR001 chuyển "Đã trả" ngày 13/05/2026. Chuyển lại tab Sách: BOOK003 hiển thị **"Có sẵn"** ngay lập tức. | **Pass** | [TC-11a (trước)](../screenshots/TC-11a_before_return.png) · [TC-11b (Mượn/Trả)](../screenshots/TC-11b_muon_tra_tab.png) · [TC-11c (sau trả)](../screenshots/TC-11c_returned.png) · [TC-11d (tab Sách)](../screenshots/TC-11d_sach_after_return.png) | — |

---

## Tổng hợp kết quả

| Chỉ số | Giá trị |
|--------|---------|
| Tổng số test case | 11 |
| Pass | 11 |
| Fail | 0 |
| Blocked | 0 |
| Not Run | 0 |
| **Tỷ lệ Pass** | **100%** |

### Kết quả theo nhóm chức năng

| Nhóm | Tổng TC | Pass | Fail | Tỷ lệ Pass |
|------|---------|------|------|------------|
| Đăng nhập (REQ-01) | 5 | 5 | 0 | 100% |
| Xem danh sách sách (REQ-02) | 6 | 6 | 0 | 100% |
| **Tổng** | **11** | **11** | **0** | **100%** |

---

## Ghi chú phát hiện

| # | Loại | Mô tả |
|---|------|-------|
| 1 | Sai khác SRS | TC-09: SRS (REQ-02) mô tả trạng thái sách mượn là **"Đã mượn"**, nhưng hệ thống thực tế hiển thị **"Đang mượn"**. Không ảnh hưởng chức năng, chỉ là thuật ngữ khác nhau.
