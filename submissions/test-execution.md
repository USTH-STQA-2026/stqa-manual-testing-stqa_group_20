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

---

## Results Summary

| Metric | Value |
|--------|-------|
| Total test cases | 11 |
| Pass | 11 |
| Fail | 0 |
| Blocked | 0 |
| Not Run | 0 |
| **Pass Rate** | **100%** |

### Results by Feature Group

| Group | Total TC | Pass | Fail | Pass Rate |
|-------|----------|------|------|-----------|
| Login (REQ-01) | 5 | 5 | 0 | 100% |
| View Book List (REQ-02) | 6 | 6 | 0 | 100% |
| **Total** | **11** | **11** | **0** | **100%** |

---

## Observations

| # | Type | Description |
|---|------|-------------|
| 1 | SRS Discrepancy | TC-09: SRS (REQ-02) describes the borrowed book status as **"Borrowed"**, but the system actually displays **"Currently Borrowed"**. No functional impact, terminology difference only. |
