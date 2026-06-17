# Test Execution — Test Execution Results

> **Instructions**: Run each TC on the system https://stqa.rbc.vn, record actual results.
> Verdict: **Pass** (correct result), **Fail** (incorrect result → create bug report), **Blocked** (cannot execute due to blocking error), **Not Run** (not yet executed).

| Info | |
|---|---|
| **Group** | `Group 20` |
| **Execution Date** | 13/05/2026 |
| **Browser** | Chrome 148.0.7778.168 |
| **Operating System** | Windows |

---

## Detailed Results

| TC ID | Feature Group | Expected Result (summary) | Actual Result | Verdict | Evidence | Bug |
|-------|---------------|--------------------------|---------------|---------|---------|-----|
| TC-01 | Login | Redirected to home page, displays name + "(Librarian)", sees 3 tabs | Redirected to home page. AppBar displays "Nguyễn Thủ Thư (Librarian)". All 3 tabs shown: Books, Borrow/Return, Members. | **Pass** | [TC-01_librarian_login.png](../screenshots/TC-01_librarian_login.png) | — |
| TC-02 | Login | Redirected to home page, displays name + "(Member)", no Members tab | Redirected to home page. AppBar displays "Nguyễn Học Bá (Member)". Only 2 tabs: Books, Borrow/Return — no Members tab. | **Pass** | [TC-02_member_login.png](../screenshots/TC-02_member_login.png) | — |
| TC-03 | Login | Login fails, message "Member not found." | Stayed on login page. Error message appeared: **"Member not found."** | **Pass** | [TC-03_email_not_found.png](../screenshots/TC-03_email_not_found.png) | — |
| TC-04 | Login | Login fails, message "Incorrect password." | Stayed on login page. Error message appeared: **"Incorrect password."** (different from the email-not-found message). | **Pass** | [TC-04_wrong_password.png](../screenshots/TC-04_wrong_password.png) | — |
| TC-05 | Login | Login fails, message "Please enter email and password." | Stayed on login page. Error message appeared: **"Please enter email and password."** | **Pass** | [TC-05_empty_fields.png](../screenshots/TC-05_empty_fields.png) | — |
| TC-06 | View Book List | Librarian sees all 20 books, each with 5 information fields | Displayed all **20/20 books** when scrolling the list (BOOK001–BOOK020). Each book has: title, author, genre, publication year, status. | **Pass** | [TC-06a (top of list)](../screenshots/TC-06a_librarian_book_list_top.png) · [TC-06b (bottom of list)](../screenshots/TC-06b_librarian_book_list_bottom.png) | — |
| TC-07 | View Book List | Member sees all 20 books, each with 5 information fields | Displayed all **20/20 books** when scrolling. Available books show an extra **+** (borrow) button; borrowed books only display a status label. | **Pass** | [TC-07a (top of list)](../screenshots/TC-07a_member_book_list_top.png) · [TC-07b (bottom of list)](../screenshots/TC-07b_member_book_list_bottom.png) | — |
| TC-08 | View Book List | BOOK001 displays status "Available" | BOOK001 (Lập trình Flutter cơ bản) displays status label: **"Available"**. | **Pass** | [TC-08_book001_co_san.png](../screenshots/TC-08_book001_co_san.png) | — |
| TC-09 | View Book List | BOOK003 displays status "Borrowed" | BOOK003 (Kiểm thử phần mềm nhập môn) displays status label: **"Borrowed"**. | **Pass** | [TC-09_book003_dang_muon.png](../screenshots/TC-09_book003_dang_muon.png) | — |
| TC-10 | View Book List | After borrowing: BOOK001 changes to "Borrowed" immediately, no refresh needed | Click **+** → Dialog: "Do you want to borrow 'Lập trình Flutter cơ bản'?" → Click **Borrow**. BOOK001 immediately changes to **"Borrowed"**. Notification **"Book borrowed successfully!"** appears. | **Pass** | [TC-10a (before)](../screenshots/TC-10a_before_borrow.png) · [TC-10b (dialog)](../screenshots/TC-10b_confirm_dialog.png) · [TC-10c (after)](../screenshots/TC-10c_after_borrow.png) | — |
| TC-11 | View Book List | After returning: BOOK003 changes to "Available" immediately, no refresh needed | Borrow/Return tab → Click **Return Book** on BR001 → Notification **"Book returned successfully."**, BR001 changes to "Returned" on 13/05/2026. Switch back to Books tab: BOOK003 displays **"Available"** immediately. | **Pass** | [TC-11a (before)](../screenshots/TC-11a_before_return.png) · [TC-11b (Borrow/Return tab)](../screenshots/TC-11b_muon_tra_tab.png) · [TC-11c (after return)](../screenshots/TC-11c_returned.png) · [TC-11d (Books tab)](../screenshots/TC-11d_sach_after_return.png) | — |
| TC-12 | Search & Filter | Displays all books containing "Flutter" in the title. | Books tab → Typed "Flutter" into search bar → Book "Lập trình Flutter cơ bản" appeared. | **Pass** | [TC-12_Tim_kiem_Flutter.png](../screenshots/TC-12_Tim_kiem_Flutter.png) | — |
| TC-13 | Search & Filter | Displays books with category "Kinh tế". | Books tab → Typed "Kinh tế" into "Filter by category" bar → System displayed 3 books of "Kinh tế" category. | **Pass** | [TC-13_Loc_Sach_KinhTe.png](../screenshots/TC-13_Loc_Sach_KinhTe.png) | — |
| TC-14 | Search & Filter | Displays only books by author Nguyễn Minh Đức. | Books tab → Typed "Nguyễn Minh Đức" into search bar → System displayed 2 books of author Nguyễn Minh Đức. | **Pass** | [TC-14_Tim_Sach_TacGia.png](../screenshots/TC-14_Tim_Sach_TacGia.png) | — |
| TC-15 | Search & Filter | Displays message: "No books found". System remains stable. | Books tab → Typed "xyz123abc!!!" into search bar → System displayed message "No books found". | **Pass** | [TC-15_Khong_Tim_Thay.png](../screenshots/TC-15_Khong_Tim_Thay.png) | — |
| TC-16 | Search & Filter | System filters accurately and displays only BOOK002. | Books tab → Typed "Cấu trúc dữ liệu và giải thuật" into search bar → System displayed only book "Cấu trúc dữ liệu và giải thuật" (BOOK002). | **Pass** | [TC-16_Tim_Kiem_100.png](../screenshots/TC-16_Tim_Kiem_100.png) | — |
| TC-17 | Search & Filter | System shows "No books found" because no book fits both the keyword and the genre filter. | Books tab → Typed "Flutter" into search bar → Typed "Kinh tế" into the filter bar → System displayed 3 books of "Kinh tế" category (the genre filter overrode the keyword). | **Fail** | [TC-17.png](../screenshots/TC-17.png) | BUG-05 |
| TC-18 | Borrow Books | Notification "Book borrowed successfully!" appears. BOOK001 status updates to "Borrowed" or "Currently Borrowed". New borrow record added to "Borrow/Return" tab with a due date 14 days from today. | Successfully borrowed BOOK001. Notification "Book borrowed successfully!" displayed, book status changed to "Currently Borrowed" in the list, and a new record was created in the Borrow/Return tab. | **Pass** | [TC-18a (dialog)](../screenshots/TC-18a_confirm_dialog.png) · [TC-18b (after)](../screenshots/TC-18b_after_borrow.png) | — |
| TC-19 | Borrow Books | The + (borrow) button is hidden or disabled for BOOK003. The status displays "Borrowed" or "Currently Borrowed". | Verified. BOOK003 displays status "Currently Borrowed", and no "+" button is visible or interactive. | **Pass** | [TC-19 (status)](../screenshots/TC-19_book003_no_button.png) | — |
| TC-20 | Borrow Books | The + (borrow) button is hidden or disabled for BOOK007. The status displays "Lost". | Verified. BOOK007 displays status "Lost", and no "+" button is visible or interactive. | **Pass** | [TC-20 (status)](../screenshots/TC-20_book007_lost.png) | — |
| TC-21 | Borrow Books | Borrowing fails. A specific error message appears: "Thành viên đang bị tạm ngưng. Không thể mượn sách." | Borrowing failed, but the error message displayed was: **"Thành viên đã hết hạn. Không thể mượn sách."** (Member is expired) instead of "Thành viên đang bị tạm ngưng...". | **Fail** | [TC-21 (wrong error)](../screenshots/TC-21_suspended_wrong_error.png) | BUG-04 |
| TC-22 | Borrow Books | Borrowing fails. A specific error message appears: "Thành viên đã hết hạn. Không thể mượn sách." | Borrowing failed. The correct error message **"Thành viên đã hết hạn. Không thể mượn sách."** was displayed on screen. | **Pass** | [TC-22 (expired error)](../screenshots/TC-22_expired_correct_error.png) | — |
| TC-23 | Borrow Books | Borrowing fails. A specific notification appears: "Đã đạt giới hạn mượn tối đa (3 sách)." | **Borrowing succeeded.** The member was allowed to borrow a 4th book, and a 4th active loan record was created under their account. | **Fail** | [TC-23 (4th borrow allowed)](../screenshots/TC-23_4th_book_allowed.png) | BUG-02 |
| TC-24 | Return Books | Return is processed successfully. Notification "Book returned successfully." appears. BOOK001 status changes to "Returned" with current date. On the Books tab, BOOK001 status changes to "Available". | Clicked "Return Book" on a newly borrowed BOOK001. Return processed successfully, notification appeared, book status changed to "Returned", and book immediately returned to "Available" on Books tab. | **Pass** | [TC-24a (before)](../screenshots/TC-24a_active_loan.png) · [TC-24b (after)](../screenshots/TC-24b_return_success.png) | — |
| TC-25 | Return Books | Return is processed successfully. Overdue warning alert is displayed. Loan status changes to "Returned" with return date. On the Books tab, BOOK003 status changes to "Available". | **Return processed successfully but no overdue warning was displayed.** The book BR001 was returned silently and status updated to "Returned" with return date, but the screen displayed absolutely no overdue alert or warning. | **Fail** | [TC-25 (no alert)](../screenshots/TC-25_return_overdue_no_alert.png) | BUG-03 |
| TC-26 | Overdue Processing | Status of record ID BR001 is updated from "Borrowed" to "Overdue". | Borrow/Return tab → All borrow records section → Click "Check overdue books" → Record ID BR001 status went from "Borrowed" to "Overdue". | **Pass** | [TC-26a_Truoc_Khi_Kiem_tra.png](../screenshots/TC-26a_Truoc_Khi_Kiem_tra.png) · [TC-26b_Sau_Khi_Kiem_tra.png](../screenshots/TC-26b_Sau_Khi_Kiem_tra.png) | — |
| TC-27 | Overdue Processing | Member sees their loan record BR001 clearly displays "Overdue". | Borrow/Return tab → My borrow records section → Record ID BR001 displayed as "Overdue". | **Pass** | [TC-27_thanh_vien_qua_han.png](../screenshots/TC-27_thanh_vien_qua_han.png) | — |
| TC-28 | Member Management | Member is created successfully, displays success message "Thêm thành viên thành công! Mã: MEM007" | Members tab → Click "+" (Add member) → Enter full name, unique valid email, phone number → Click "Thêm thành viên" → Member created successfully, displayed success toast message. | **Pass** | [TC-28_success_member.png](../screenshots/TC-28_success_member.png) | — |
| TC-29 | Member Management | Creation is rejected. Error message appears: "Email không hợp lệ." | Members tab → Click "+" (Add member) → Enter "Test Name One", invalid email "testemail@domain" (no dot in domain), phone number → Click "Thêm thành viên". **Creation succeeded instead of being rejected.** | **Fail** | [TC-29_invalid_email_format.png](../screenshots/TC-29_invalid_email_format.png) | BUG-06 |
| TC-30 | Member Management | Creation is rejected. A specific error message appears: "Email đã tồn tại." | Members tab → Click "+" (Add member) → Enter "Test Duplicate", duplicate email "ba.nguyen@email.com", phone number → Click "Thêm thành viên". **Creation rejected but with incorrect generic message "Email không hợp lệ" instead of duplicate warning.** | **Fail** | [TC-30_duplicate_email.png](../screenshots/TC-30_duplicate_email.png) | BUG-07 |
| TC-31 | Member Management | The Members tab is hidden, member cannot access the member management features. | Logged in as Member (MEM002). Verified the tab bar contains only "Sách" and "Mượn / Trả" tabs; the "Thành viên" tab is completely hidden. | **Pass** | [TC-31_member_no_members_tab.png](../screenshots/TC-31_member_no_members_tab.png) | — |
| TC-32 | Borrow Record Lookup | Librarian can see the complete list of borrow records of all members. | Logged in as Librarian (librarian@library.com) → Switch to "Mượn / Trả" tab → Checked all borrow records section. All records of all members are displayed. | **Pass** | [TC-32_librarian_all_loans.png](../screenshots/TC-32_librarian_all_loans.png) | — |
| TC-33 | Borrow Record Lookup | Member only sees their own records (e.g. BR001 and BR004). | Logged in as Member (MEM002) → Switch to "Mượn / Trả" tab → Verified "Phiếu mượn của tôi" tab. Only personal records BR001 and BR004 are listed. | **Pass** | [TC-33_member_own_loans.png](../screenshots/TC-33_member_own_loans.png) | — |
| TC-34 | Borrow Record Lookup | Access is denied or search returns no results, member is blocked from viewing other members' borrow records. | Logged in as Member (MEM002) → Switch to "Mượn / Trả" tab → Click "Tra cứu phiếu mượn" tab → Enter MEM003 → Click "Tra cứu". **Search successfully retrieved and displayed MEM003's borrow records, leaking their private data.** | **Fail** | [TC-34_member_view_others_loans.png](../screenshots/TC-34_member_view_others_loans.png) | BUG-08 |
---

## Results Summary

| Metric | Value |
|--------|-------|
| Total test cases | 34 |
| Pass | 27 |
| Fail | 7 |
| Blocked | 0 |
| Not Run | 0 |
| **Pass Rate** | **79.4%**  |

### Results by Feature Group

| Group | Total TC | Pass | Fail | Pass Rate |
|-------|----------|------|------|-----------|
| Login (REQ-01) | 5 | 5 | 0 | 100% |
| View Book List (REQ-02) | 6 | 6 | 0 | 100% |
| Search & Filter (REQ-03) | 6 | 5 | 1 | 83.3% |
| Borrow Books (REQ-04) | 6 | 4 | 2 | 66.7% |
| Return Books (REQ-05) | 2 | 1 | 1 | 50.0% |
| Overdue Processing (REQ-06) | 2 | 2 | 0 | 100% |
| Member Management (REQ-07) | 4 | 2 | 2 | 50.0% |
| Borrow Record Lookup (REQ-08) | 3 | 2 | 1 | 66.7% |
| **Total** | **34** | **27** | **7** | **79.4%** |

---

## Observations

| # | Type | Description |
|---|------|-------------|
| 1 | SRS Discrepancy | TC-09: SRS (REQ-02) describes the borrowed book status as **"Borrowed"**, but the system actually displays **"Currently Borrowed"**. No functional impact, terminology difference only. |
