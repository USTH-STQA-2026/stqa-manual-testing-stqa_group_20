# Test Cases

> **Instructions**: Write a minimum of **20 TC** covering all main features (REQ-01 → REQ-08).
> See [examples/sample-test-case.md](../examples/sample-test-case.md) to understand how to write good TCs.
> Organize and group test cases in the most appropriate way.

| Info | |
|---|---|
| **Group** | `Group 20` |
| **Date Created** | `13/05/2026` |
| **System** | https://stqa.rbc.vn |
| **Reference** | SRS v1.0 |

---

## Step 1: Input Domain Modeling (IDM)

> 📖 **Textbook:** Chapter 6 — *Input Domain Modeling*, Paul Ammann & Jeff Offutt.
>
> **Before writing Test Cases**, the team **must** analyze the input domain using the IDM table below.
> For each feature, identify: **Characteristic**, **Block/Partition**, and **Representative Value**.

### IDM — Login (REQ-01)

| Characteristic | Block | Representative Value | Expected Result |
|---|---|---|---|
| Email exists in DB? | Yes | `librarian@library.com` | Login successful |
| | No | `noone@email.com` | Error message |
| Password correct? | Correct | `admin123` | Login successful |
| | Wrong | `wrongpass` | Error message |
| Input field empty? | Not empty | (any value) | Processed normally |
| | Empty | `""` | Message: "Please enter…" |

### IDM — View Book List (REQ-02)

| Characteristic | Block | Representative Value | Expected Result |
|---|---|---|---|
| User role? | Librarian | LIB001 | Can view the complete book list |
| | Member | MEM002 | Can view the complete book list |
| Book status displayed? | Available | BOOK001 | Displays "Available" |
| | Borrowed | BOOK003 | Displays "Borrowed" |
| | Lost | BOOK007 | Displays "Lost" |
| Information per book? | All 5 fields complete | (any book) | Displays: title, author, genre, publication year, status |
| Real-time update? | After borrowing | BOOK001 just borrowed | Status immediately → "Borrowed" (no refresh needed) |
| | After returning | BOOK003 just returned | Status immediately → "Available" (no refresh needed) |

### IDM — Search Books (REQ-03)

| Characteristic | Block | Representative Value | Expected Result |
|---|---|---|---|
| Keyword exists in DB? | Yes (book title) | `"Flutter"` | Displays books containing "Flutter" |
| | Yes (author name) | `"Nguyễn"` | Displays books by author Nguyễn |
| | No | `"XYZ123"` | Empty list |
| Case-sensitive? | Lowercase | `"flutter"` | Same results as "Flutter" |
| | Uppercase | `"FLUTTER"` | Same results as "Flutter" |

### IDM — Borrow Books (REQ-04, REQ-05)

| Characteristic | Block | Representative Value | Expected Result |
|---|---|---|---|
| Book status? | Available | BOOK001 | Borrowing allowed |
| | Currently borrowed | BOOK003 | Not allowed |
| | Lost | BOOK007 | Not allowed |
| Member status? | Active | MEM002 | Borrowing allowed |
| | Suspended | MEM004 | Rejected, error message |
| | Expired | MEM005 | Rejected, error message |
| Number of books currently borrowed? | < 3 (BVA: 0, 1, 2) | MEM006 (0 books) | Borrowing allowed |
| | = 3 (BVA: limit) | Member has borrowed 3 books | Rejected, limit exceeded notification |

### IDM — Return Books (REQ-05)

| Characteristic | Block | Representative Value | Expected Result |
|---|---|---|---|
| Return timing? | On-time | Return date <= due date | Return successful, no alert |
| | Overdue | Return date > due date | Return successful, overdue warning alert |
| User authorization? | Own record | Return own book | Allowed |
| | Other's record | Return someone else's book | Action unavailable (not visible) |

### IDM — Member Management (REQ-07)

| Characteristic | Block | Representative Value | Expected Result |
|---|---|---|---|
| User Authorization? | Librarian | LIB001 | Allowed to access tab & add member |
| | Member | MEM002 | Access denied (tab not visible) |
| Email format valid? | Valid format | `newmember@email.com` | Created successfully |
| | Invalid (no @) | `newmember.email.com` | Rejected, error message |
| | Invalid (no dot in domain) | `newmember@email` | Rejected, error message |
| Email uniqueness? | Unique | `newmember@email.com` | Created successfully |
| | Duplicate | `ba.nguyen@email.com` | Rejected, error message |

### IDM — Borrow Record Lookup (REQ-08)

| Characteristic | Block | Representative Value | Expected Result |
|---|---|---|---|
| User Authorization? | Librarian | LIB001 | Allowed to view all members' records |
| | Member | MEM002 | Allowed to view only own records |
| Record access? | Own record | MEM002 looks up MEM002 | Allowed |
| | Other's record | MEM002 looks up MEM003 | Rejected (unauthorized/hidden) |

> 💡 **Technical tip**: Use **Equivalence Partitioning (EP)** for discrete partitions, **Boundary Value Analysis (BVA)** for numeric partitions (e.g., the 3-book limit). See textbook §6.1–6.3.

---

## Step 2: Test Cases

<!-- Organize the test case table freely: by feature, by REQ, or by business flow — team's choice. -->
<!-- Each TC must map back to at least 1 row in the IDM table in Step 1. -->

### Login (REQ-01)

| TC ID | Test Objective | Precondition | Steps | Input Data | Expected Result | REQ | Technique | Evidence |
|-------|----------------|--------------|-------|------------|-----------------|-----|-----------|----------|
| TC-01 | Successful login — Librarian account | Login page is displayed, not yet logged in | 1. Enter email in the **Email** field. 2. Enter password in the **Password** field. 3. Click the **Login** button. | Email: `librarian@library.com` / Password: `admin123` | Redirected to the home page. System correctly identifies Librarian role: displays name + "(Librarian)", all 3 features accessible: Books, Borrow/Return, Members. | REQ-01 | EP | [TC-01_librarian_login.png](../screenshots/TC-01_librarian_login.png) |
| TC-02 | Successful login — Member account | Login page is displayed, not yet logged in | 1. Enter email in the **Email** field. 2. Enter password in the **Password** field. 3. Click the **Login** button. | Email: `ba.nguyen@email.com` / Password: `password123` | Redirected to the home page. System correctly identifies Member role: displays name + "(Member)", **cannot** access the Members feature (Librarian only). | REQ-01 | EP | [TC-02_member_login.png](../screenshots/TC-02_member_login.png) |
| TC-03 | Login with email that does not exist in the system | Login page is displayed, not yet logged in | 1. Enter a non-existent email in the **Email** field. 2. Enter any password in the **Password** field. 3. Click the **Login** button. | Email: `randomuser@gmail.com` / Password: `qweqweqwe` | Login fails, stays on the login page. Error message: **"Member not found."** | REQ-01 | EP | [TC-03_email_not_found.png](../screenshots/TC-03_email_not_found.png) |
| TC-04 | Login with wrong password (correct email) | Login page is displayed, not yet logged in | 1. Enter a valid email in the **Email** field. 2. Enter the **wrong** password in the **Password** field. 3. Click the **Login** button. | Email: `librarian@library.com` / Password: `qweqweqwe` | Login fails, stays on the login page. Error message: **"Incorrect password."** — distinct from the email-not-found message. | REQ-01 | EP | [TC-04_wrong_password.png](../screenshots/TC-04_wrong_password.png) |
| TC-05 | Login with both fields left empty | Login page is displayed, not yet logged in | 1. Leave the **Email** field empty. 2. Leave the **Password** field empty. 3. Click the **Login** button. | Email: *(empty)* / Password: *(empty)* | Login fails, stays on the login page. Error message: **"Please enter email and password."** | REQ-01 | EP | [TC-05_empty_fields.png](../screenshots/TC-05_empty_fields.png) |

### View Book List (REQ-02)

| TC ID | Test Objective | Precondition | Steps | Input Data | Expected Result | REQ | Technique | Evidence |
|-------|----------------|--------------|-------|------------|-----------------|-----|-----------|----------|
| TC-06 | Librarian views book list — displays all 20 books with complete information for each book | Logged in as Librarian, currently on the **Books** tab | 1. Observe the book list on screen. 2. Count the number of books displayed. 3. Verify the information of any book (e.g., BOOK001). | Account: `librarian@library.com` / `admin123` | The list displays all **20 books**. Each book has all 5 fields: **title**, **author**, **genre**, **publication year**, **status**. | REQ-02 | EP | [TC-06a](../screenshots/TC-06a_librarian_book_list_top.png) · [TC-06b](../screenshots/TC-06b_librarian_book_list_bottom.png) |
| TC-07 | Member views book list — displays all 20 books with complete information for each book | Logged in as Member, currently on the **Books** tab | 1. Observe the book list on screen. 2. Count the number of books displayed. 3. Verify the information of any book (e.g., BOOK001). | Account: `ba.nguyen@email.com` / `password123` | The list displays all **20 books**. Each book has all 5 fields: **title**, **author**, **genre**, **publication year**, **status**. | REQ-02 | EP | [TC-07a](../screenshots/TC-07a_member_book_list_top.png) · [TC-07b](../screenshots/TC-07b_member_book_list_bottom.png) |
| TC-08 | Book with "Available" status displays correct status | Logged in (any role), currently on the **Books** tab, data in initial state (seed data) | 1. Find **BOOK001** (Lập trình Flutter cơ bản) in the list. 2. Read the displayed status of this book. | Book: BOOK001 — initial status per seed data is **Available** | The status of BOOK001 is displayed as **"Available"**. | REQ-02 | EP | [TC-08_book001_co_san.png](../screenshots/TC-08_book001_co_san.png) |
| TC-09 | Book currently on loan displays correct status "Borrowed" | Logged in (any role), currently on the **Books** tab, data in initial state (seed data) | 1. Find **BOOK003** (Kiểm thử phần mềm nhập môn) in the list. 2. Read the displayed status of this book. | Book: BOOK003 — initial status per seed data is currently borrowed by MEM002 | The status of BOOK003 is displayed as **"Borrowed"**. | REQ-02 | EP | [TC-09_book003_dang_muon.png](../screenshots/TC-09_book003_dang_muon.png) |
| TC-10 | Book status updates in real-time immediately after Member borrows — no page refresh required | Logged in as Member (MEM002), currently on the **Books** tab, BOOK001 is in "Available" status | 1. Confirm BOOK001 displays status **"Available"**. 2. Click the **+** button next to BOOK001. 3. Confirmation dialog appears — click **Borrow**. 4. Observe BOOK001's status immediately without refreshing the page. | Book: BOOK001 / Account: `ba.nguyen@email.com` / `password123` | Confirmation dialog: "Do you want to borrow 'Lập trình Flutter cơ bản'?". After confirming: BOOK001 status **immediately changes to "Borrowed"**, notification **"Book borrowed successfully!"** appears. | REQ-02 | EP | [TC-10a](../screenshots/TC-10a_before_borrow.png) · [TC-10b](../screenshots/TC-10b_confirm_dialog.png) · [TC-10c](../screenshots/TC-10c_after_borrow.png) |
| TC-11 | Book status updates in real-time immediately after Librarian processes return — no page refresh required | Logged in as Librarian, initial data: BOOK003 is in "Borrowed" status (loan record BR001 of MEM002) | 1. On the **Books** tab: confirm BOOK003 displays **"Borrowed"**. 2. Switch to the **Borrow/Return** tab. 3. Find record BR001 (Kiểm thử phần mềm nhập môn — Borrowed), click the **Return Book** button. 4. Switch back to the **Books** tab, observe BOOK003's status. | Loan record: BR001 / Book: BOOK003 | BR001 changes to status **"Returned"** with the return date recorded. Notification **"Book returned successfully."** appears. On the Books tab: BOOK003 **immediately changes to "Available"** without needing to refresh the page. | REQ-02 | EP | [TC-11a](../screenshots/TC-11a_before_return.png) · [TC-11b](../screenshots/TC-11b_muon_tra_tab.png) · [TC-11c](../screenshots/TC-11c_returned.png) · [TC-11d](../screenshots/TC-11d_sach_after_return.png) |

### Search & Filter (REQ-03)

| TC ID | Test Objective | Precondition | Steps | Input Data | Expected Result | REQ | Technique | Evidence |
|-------|----------------|--------------|-------|------------|-----------------|-----|-----------|----------|
| TC-20 | Basic search by Book Title | Logged in as Member (MEM002), currently on **Books** tab | 1. Navigate to Search bar. 2. Enter part of a book title (BOOK001) into the search bar. | Input: `Flutter` | System displays all books containing "Flutter" in the title. | REQ-03 | EP | [TC-20_Tim_kiem_Flutter.png](../screenshots/TC-20_Tim_kiem_Flutter.png) |
| TC-21 | Filter books by Genre | Logged in as Member (MEM002), currently on **Books** tab | 1. Navigate to Filter bar. 2. Enter the genre to filter. | Genre: `Economy` (Kinh Tế) | System only displays books with the genre "Economy". | REQ-03 | EP | [TC-21_Loc_Sach_KinhTe.png](../screenshots/TC-21_Loc_Sach_KinhTe.png) |
| TC-22 | Basic search by Author name | Logged in as Member (MEM002), currently on **Books** tab | 1. Navigate to Search bar. 2. Enter author name into the search bar. | Author: `Nguyễn Minh Đức` | System only displays books by author Nguyễn Minh Đức. | REQ-03 | EP | [TC-22_Tim_Sach_TacGia.png](../screenshots/TC-22_Tim_Sach_TacGia.png) |
| TC-23 | Handling when no results are found | Logged in as Member (MEM002), currently on **Books** tab | 1. Enter a random, non-existent string into the search bar. 2. Click "Search" button. | Input: `xyz123abc!!!` | System displays message: "No books found". System remains stable. | REQ-03 | EP | [TC-23_Khong_Tim_Thay.png](../screenshots/TC-23_Khong_Tim_Thay.png) |
| TC-24 | Search with 100% exact keyword match | Logged in as Member (MEM002), currently on **Books** tab | 1. Copy the exact full book title. 2. Paste into the Search box. | Input: `Cấu trúc dữ liệu và giải thuật` | System filters accurately and displays only **BOOK002**. | REQ-03 | BVA | [TC-24_Tim_Kiem_100.png](../screenshots/TC-24_Tim_Kiem_100.png) |
| TC-27 | Filter by category and search combination | Logged in as Member (MEM002), currently on **Books** tab | 1. Enter "Flutter" into the search bar. 2. Enter "Kinh tế" in "Filter by category" | Input search bar: `Flutter`/ Input filter: `Kinh tế` | System show "No books found" because no book fit those requirements | REQ-03 | EP | [TC-27.png](../screenshots/TC-27.png) |

### Borrow Books (REQ-04)

| TC ID | Test Objective | Precondition | Steps | Input Data | Expected Result | REQ | Technique | Evidence |
|-------|----------------|--------------|-------|------------|-----------------|-----|-----------|----------|
| TC-12 | Successful Borrowing - Active Member | Logged in as Active Member (`ba.nguyen@email.com`), currently on Books tab, `BOOK001` is "Available", holding < 3 books | 1. Locate book `BOOK001`. 2. Click the **+** (borrow) button. 3. Click **Borrow** on the confirmation dialog. | Book: `BOOK001` / Account: `ba.nguyen@email.com` | Borrowing succeeds. A notification "Book borrowed successfully!" appears. Book status updates to "Borrowed" (or "Currently Borrowed"). A new borrow record is added under "Borrow/Return" tab with a due date 14 days from today. | REQ-04 | EP | [TC-12a](../screenshots/TC-12a_confirm_dialog.png) · [TC-12b](../screenshots/TC-12b_after_borrow.png) |
| TC-13 | Rejection - Borrowing an already borrowed book | Logged in as Active Member (`ba.nguyen@email.com`), currently on Books tab | 1. Locate book `BOOK003` (which is already borrowed in seed data). 2. Observe the action button next to it. | Book: `BOOK003` | The **+** (borrow) button is hidden or disabled for `BOOK003`. The status label displays "Borrowed" (or "Currently Borrowed") and no borrow action can be performed. | REQ-04 | EP | [TC-13](../screenshots/TC-13_book003_no_button.png) |
| TC-14 | Rejection - Borrowing a lost book | Logged in as Active Member (`ba.nguyen@email.com`), currently on Books tab | 1. Locate book `BOOK007` (which is "Lost" in seed data). 2. Observe the action button next to it. | Book: `BOOK007` | The **+** (borrow) button is hidden or disabled for `BOOK007`. The status label displays "Lost" and no borrow action can be performed. | REQ-04 | EP | [TC-14](../screenshots/TC-14_book007_lost.png) |
| TC-15 | Rejection - Suspended Member attempts to borrow | Logged in as Suspended Member (`cu.le@email.com`), currently on Books tab, `BOOK001` is "Available" | 1. Locate book `BOOK001`. 2. Click the **+** (borrow) button. 3. Click **Borrow** on the confirmation dialog. | Book: `BOOK001` / Account: `cu.le@email.com` | Borrowing is rejected. A specific error message appears: "Thành viên đang bị tạm ngưng. Không thể mượn sách." (or "Member is suspended. Cannot borrow book."). Book status remains "Available". | REQ-04 | EP | [TC-15](../screenshots/TC-15_suspended_wrong_error.png) |
| TC-16 | Rejection - Expired Member attempts to borrow | Logged in as Expired Member (`binh.pham@email.com`), currently on Books tab, `BOOK001` is "Available" | 1. Locate book `BOOK001`. 2. Click the **+** (borrow) button. 3. Click **Borrow** on the confirmation dialog. | Book: `BOOK001` / Account: `binh.pham@email.com` | Borrowing is rejected. A specific error message appears: "Thành viên đã hết hạn. Không thể mượn sách." (or "Member is expired. Cannot borrow book."). Book status remains "Available". | REQ-04 | EP | [TC-16](../screenshots/TC-16_expired_correct_error.png) |
| TC-17 | Rejection - Limit Exceeded (Borrowing 4th book) | Logged in as Active Member (`ba.nguyen@email.com`), currently on Books tab, data in initial state (holds 1 book: `BOOK003` in seed data) | 1. Borrow two available books (e.g., `BOOK001` and `BOOK002`) by clicking **+** and confirming, reaching the limit of 3 books. 2. Locate a 4th available book (e.g., `BOOK005`). 3. Click the **+** (borrow) button next to `BOOK005`. 4. Click **Borrow** on the confirmation dialog. | Books: `BOOK001`, `BOOK002` (to reach limit), then `BOOK005` (4th book) / Account: `ba.nguyen@email.com` | Borrowing of `BOOK005` fails. A specific notification appears: "Đã đạt giới hạn mượn tối đa (3 sách)." (or "Maximum borrow limit reached (3 books)."). Book `BOOK005` status remains "Available". | REQ-04 | BVA | [TC-17](../screenshots/TC-17_4th_book_allowed.png) |

### Return Books (REQ-05)

| TC ID | Test Objective | Precondition | Steps | Input Data | Expected Result | REQ | Technique | Evidence |
|-------|----------------|--------------|-------|------------|-----------------|-----|-----------|----------|
| TC-18 | Successful Return - On-Time (No Overdue Alert) | Logged in as Active Member (`ba.nguyen@email.com`), currently has an active, on-time loan for `BOOK001` | 1. Switch to **Borrow/Return** tab. 2. Locate active record for `BOOK001` (within 14-day limit). 3. Click the **Return Book** button next to it. | Book: `BOOK001` / Account: `ba.nguyen@email.com` | Return is processed successfully. Notification "Book returned successfully." appears. The book's status in the list changes to "Returned" with current date. On the Books tab, `BOOK001` status immediately changes to "Available". No overdue alert is shown. | REQ-05 | EP | [TC-18a](../screenshots/TC-18a_active_loan.png) · [TC-18b](../screenshots/TC-18b_return_success.png) |
| TC-19 | Successful Return - Overdue Book (Triggers Overdue Warning Alert) | Logged in as Active Member (`ba.nguyen@email.com`), has overdue seed loan record `BR001` | 1. Switch to **Borrow/Return** tab. 2. Locate record `BR001` (`BOOK003` - Overdue). 3. Click the **Return Book** button next to it. | Book: `BOOK003` / Account: `ba.nguyen@email.com` | Return is processed successfully. An **overdue warning alert** is displayed on the screen (e.g., warning that the book was returned late). The loan status updates to "Returned" with return date. On the Books tab, `BOOK003` immediately changes to "Available". | REQ-05 | EP, BVA | [TC-19](../screenshots/TC-19_return_overdue_no_alert.png) |

### Overdue Processing (REQ-06)

| TC ID | Test Objective | Precondition | Steps | Input Data | Expected Result | REQ | Technique | Evidence |
|-------|----------------|--------------|-------|------------|-----------------|-----|-----------|----------|
| TC-25 | Librarian scans and updates status for overdue loans | Logged in as Librarian, system has existing overdue loans. | 1. Go to Librarian's **Borrow/Return** tab. 2. Select **All Loans**. 3. Click **Check Overdue Books** button. | Account: `librarian@library.com` / `admin123`. Target: **BR001** (Due date: 15/09/2024) | Status of record **BR001** is successfully updated from "Borrowed" to "Overdue". | REQ-06 | EP | [TC-25a_Truoc_Khi_Kiem_tra.png](../screenshots/TC-25a_Truoc_Khi_Kiem_tra.png) · [TC-25b_Sau_Khi_Kiem_tra.png](../screenshots/TC-25b_Sau_Khi_Kiem_tra.png) |
| TC-26 | Verify overdue status visibility for Member account | Librarian has clicked "Check Overdue Books". Logged in as Member (MEM002). | 1. Navigate to **Borrow/Return** tab. 2. Select **My Loans**. | Account: `ba.nguyen@email.com` / `password123` (Owner of BR001) | Member sees their personal loan list and record BR001 clearly displays "Overdue". | REQ-06 | EP | [TC-26_thanh_vien_qua_han.png](../screenshots/TC-26_thanh_vien_qua_han.png) |

### Member Management (REQ-07)

| TC ID | Test Objective | Precondition | Steps | Input Data | Expected Result | REQ | Technique | Evidence |
|-------|----------------|--------------|-------|------------|-----------------|-----|-----------|----------|
| TC-28 | Successful Member Creation | Logged in as Librarian, currently on **Members** tab | 1. Click **+** (Add Member) button. 2. Enter full name. 3. Enter unique valid email. 4. Enter phone number. 5. Click **Thêm thành viên**. | Name: `Nguyễn Đinh Phú Vinh`, Email: `phuvinh.new@email.com`, Phone: `0909090909` | Member is created successfully, displays success message "Thêm thành viên thành công! Mã: MEM007" | REQ-07 | EP | [TC-28_success_member.png](../screenshots/TC-28_success_member.png) |
| TC-29 | Rejection - Add member with invalid email format (missing dot in domain) | Logged in as Librarian, currently on **Members** tab | 1. Click **+** (Add Member) button. 2. Enter full name. 3. Enter email without dot in domain. 4. Enter phone number. 5. Click **Thêm thành viên**. | Name: `Test Name One`, Email: `testemail@domain`, Phone: `0987654321` | Creation is rejected. Error message appears: "Email không hợp lệ." | REQ-07 | EP | [TC-29_invalid_email_format.png](../screenshots/TC-29_invalid_email_format.png) |
| TC-30 | Rejection - Add member with duplicate email | Logged in as Librarian, currently on **Members** tab | 1. Click **+** (Add Member) button. 2. Enter full name. 3. Enter a duplicate email. 4. Enter phone number. 5. Click **Thêm thành viên**. | Name: `Test Duplicate`, Email: `ba.nguyen@email.com`, Phone: `0987654321` | Creation is rejected. A specific error message appears: "Email đã tồn tại." | REQ-07 | EP | [TC-30_duplicate_email.png](../screenshots/TC-30_duplicate_email.png) |
| TC-31 | Security - Member account cannot access Member Management | Logged in as Member | 1. Observe the main tab bar. 2. Verify visibility of the **Members** tab. | Account: `ba.nguyen@email.com` | The **Members** tab is hidden, member cannot access the member management features. | REQ-07 | EP | [TC-31_member_no_members_tab.png](../screenshots/TC-31_member_no_members_tab.png) |

### Borrow Record Lookup (REQ-08)

| TC ID | Test Objective | Precondition | Steps | Input Data | Expected Result | REQ | Technique | Evidence |
|-------|----------------|--------------|-------|------------|-----------------|-----|-----------|----------|
| TC-32 | Librarian views all borrow records | Logged in as Librarian | 1. Go to **Borrow/Return** tab. 2. Verify all borrow records of all members are displayed. | Account: `librarian@library.com` | Librarian can see the complete list of borrow records of all members. | REQ-08 | EP | [TC-32_librarian_all_loans.png](../screenshots/TC-32_librarian_all_loans.png) |
| TC-33 | Member views own borrow records | Logged in as Member | 1. Go to **Borrow/Return** tab. 2. Verify "My Loans" shows only own borrow records. | Account: `ba.nguyen@email.com` | Member only sees their own records (e.g. BR001 and BR004). | REQ-08 | EP | [TC-33_member_own_loans.png](../screenshots/TC-33_member_own_loans.png) |
| TC-34 | Security - Member cannot lookup other members' borrow records | Logged in as Member | 1. Go to **Borrow/Return** tab. 2. Click **Tra cứu phiếu mượn** tab. 3. Enter another member's ID. 4. Click **Tra cứu**. | Account: `ba.nguyen@email.com`, Search target: `MEM003` | Access is denied or search returns no results, member is blocked from viewing other members' borrow records. | REQ-08 | EP | [TC-34_member_view_others_loans.png](../screenshots/TC-34_member_view_others_loans.png) |

---

## Summary

| Feature Group | TC Count | REQ Coverage | IDM Technique Applied |
|---------------|----------|--------------|----------------------|
| Login | 5 | REQ-01 | EP |
| View Book List | 6 | REQ-02 | EP |
| Search & Filter | 6 | REQ-03 | EP, BVA |
| Borrow Books | 6 | REQ-04 | EP, BVA |
| Return Books | 2 | REQ-05 | EP, BVA |
| Overdue Processing | 2 | REQ-06 | EP |
| Member Management | 4 | REQ-07 | EP |
| Borrow Record Lookup | 3 | REQ-08 | EP |
| **Total** | **34** | REQ-01, REQ-02, REQ-03, REQ-04, REQ-05, REQ-06, REQ-07, REQ-08 | EP, BVA |
