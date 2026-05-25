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

> 💡 **Technical tip**: Use **Equivalence Partitioning (EP)** for discrete partitions, **Boundary Value Analysis (BVA)** for numeric partitions (e.g., the 3-book limit). See textbook §6.1–6.3.

---

## Step 2: Test Cases

<!-- Organize the test case table freely: by feature, by REQ, or by business flow — team's choice. -->
<!-- Each TC must map back to at least 1 row in the IDM table in Step 1. -->

| TC ID | Test Objective | Precondition | Steps | Input Data | Expected Result | REQ | Technique |
|-------|----------------|--------------|-------|------------|-----------------|-----|-----------|
| TC-01 | Successful login — Librarian account | Login page is displayed, not yet logged in | 1. Enter email in the **Email** field. 2. Enter password in the **Password** field. 3. Click the **Login** button. | Email: `librarian@library.com` / Password: `admin123` | Redirected to the home page. System correctly identifies Librarian role: displays name + "(Librarian)", all 3 features accessible: Books, Borrow/Return, Members. | REQ-01 | EP |
| TC-02 | Successful login — Member account | Login page is displayed, not yet logged in | 1. Enter email in the **Email** field. 2. Enter password in the **Password** field. 3. Click the **Login** button. | Email: `ba.nguyen@email.com` / Password: `password123` | Redirected to the home page. System correctly identifies Member role: displays name + "(Member)", **cannot** access the Members feature (Librarian only). | REQ-01 | EP |
| TC-03 | Login with email that does not exist in the system | Login page is displayed, not yet logged in | 1. Enter a non-existent email in the **Email** field. 2. Enter any password in the **Password** field. 3. Click the **Login** button. | Email: `randomuser@gmail.com` / Password: `qweqweqwe` | Login fails, stays on the login page. Error message: **"Member not found."** | REQ-01 | EP |
| TC-04 | Login with wrong password (correct email) | Login page is displayed, not yet logged in | 1. Enter a valid email in the **Email** field. 2. Enter the **wrong** password in the **Password** field. 3. Click the **Login** button. | Email: `librarian@library.com` / Password: `qweqweqwe` | Login fails, stays on the login page. Error message: **"Incorrect password."** — distinct from the email-not-found message. | REQ-01 | EP |
| TC-05 | Login with both fields left empty | Login page is displayed, not yet logged in | 1. Leave the **Email** field empty. 2. Leave the **Password** field empty. 3. Click the **Login** button. | Email: *(empty)* / Password: *(empty)* | Login fails, stays on the login page. Error message: **"Please enter email and password."** | REQ-01 | EP |
| TC-06 | Librarian views book list — displays all 20 books with complete information for each book | Logged in as Librarian, currently on the **Books** tab | 1. Observe the book list on screen. 2. Count the number of books displayed. 3. Verify the information of any book (e.g., BOOK001). | Account: `librarian@library.com` / `admin123` | The list displays all **20 books**. Each book has all 5 fields: **title**, **author**, **genre**, **publication year**, **status**. | REQ-02 | EP |
| TC-07 | Member views book list — displays all 20 books with complete information for each book | Logged in as Member, currently on the **Books** tab | 1. Observe the book list on screen. 2. Count the number of books displayed. 3. Verify the information of any book (e.g., BOOK001). | Account: `ba.nguyen@email.com` / `password123` | The list displays all **20 books**. Each book has all 5 fields: **title**, **author**, **genre**, **publication year**, **status**. | REQ-02 | EP |
| TC-08 | Book with "Available" status displays correct status | Logged in (any role), currently on the **Books** tab, data in initial state (seed data) | 1. Find **BOOK001** (Lập trình Flutter cơ bản) in the list. 2. Read the displayed status of this book. | Book: BOOK001 — initial status per seed data is **Available** | The status of BOOK001 is displayed as **"Available"**. | REQ-02 | EP |
| TC-09 | Book currently on loan displays correct status "Borrowed" | Logged in (any role), currently on the **Books** tab, data in initial state (seed data) | 1. Find **BOOK003** (Kiểm thử phần mềm nhập môn) in the list. 2. Read the displayed status of this book. | Book: BOOK003 — initial status per seed data is currently borrowed by MEM002 | The status of BOOK003 is displayed as **"Borrowed"**. | REQ-02 | EP |
| TC-10 | Book status updates in real-time immediately after Member borrows — no page refresh required | Logged in as Member (MEM002), currently on the **Books** tab, BOOK001 is in "Available" status | 1. Confirm BOOK001 displays status **"Available"**. 2. Click the **+** button next to BOOK001. 3. Confirmation dialog appears — click **Borrow**. 4. Observe BOOK001's status immediately without refreshing the page. | Book: BOOK001 / Account: `ba.nguyen@email.com` / `password123` | Confirmation dialog: "Do you want to borrow 'Lập trình Flutter cơ bản'?". After confirming: BOOK001 status **immediately changes to "Borrowed"**, notification **"Book borrowed successfully!"** appears. | REQ-02 | EP |
| TC-11 | Book status updates in real-time immediately after Librarian processes return — no page refresh required | Logged in as Librarian, initial data: BOOK003 is in "Borrowed" status (loan record BR001 of MEM002) | 1. On the **Books** tab: confirm BOOK003 displays **"Borrowed"**. 2. Switch to the **Borrow/Return** tab. 3. Find record BR001 (Kiểm thử phần mềm nhập môn — Borrowed), click the **Return Book** button. 4. Switch back to the **Books** tab, observe BOOK003's status. | Loan record: BR001 / Book: BOOK003 | BR001 changes to status **"Returned"** with the return date recorded. Notification **"Book returned successfully."** appears. On the Books tab: BOOK003 **immediately changes to "Available"** without needing to refresh the page. | REQ-02 | EP |

| TC-12 | Successful Borrowing - Active Member | Logged in as Active Member (`ba.nguyen@email.com`), currently on Books tab, `BOOK001` is "Available", holding < 3 books | 1. Locate book `BOOK001`. 2. Click the **+** (borrow) button. 3. Click **Borrow** on the confirmation dialog. | Book: `BOOK001` / Account: `ba.nguyen@email.com` | Borrowing succeeds. A notification "Book borrowed successfully!" appears. Book status updates to "Borrowed" (or "Currently Borrowed"). A new borrow record is added under "Borrow/Return" tab with a due date 14 days from today. | REQ-04 | EP |
| TC-13 | Rejection - Borrowing an already borrowed book | Logged in as Active Member (`ba.nguyen@email.com`), currently on Books tab | 1. Locate book `BOOK003` (which is already borrowed in seed data). 2. Observe the action button next to it. | Book: `BOOK003` | The **+** (borrow) button is hidden or disabled for `BOOK003`. The status label displays "Borrowed" (or "Currently Borrowed") and no borrow action can be performed. | REQ-04 | EP |
| TC-14 | Rejection - Borrowing a lost book | Logged in as Active Member (`ba.nguyen@email.com`), currently on Books tab | 1. Locate book `BOOK007` (which is "Lost" in seed data). 2. Observe the action button next to it. | Book: `BOOK007` | The **+** (borrow) button is hidden or disabled for `BOOK007`. The status label displays "Lost" and no borrow action can be performed. | REQ-04 | EP |
| TC-15 | Rejection - Suspended Member attempts to borrow | Logged in as Suspended Member (`cu.le@email.com`), currently on Books tab, `BOOK001` is "Available" | 1. Locate book `BOOK001`. 2. Click the **+** (borrow) button. 3. Click **Borrow** on the confirmation dialog. | Book: `BOOK001` / Account: `cu.le@email.com` | Borrowing is rejected. A specific error message appears: "Thành viên đang bị tạm ngưng. Không thể mượn sách." (or "Member is suspended. Cannot borrow book."). Book status remains "Available". | REQ-04 | EP |
| TC-16 | Rejection - Expired Member attempts to borrow | Logged in as Expired Member (`binh.pham@email.com`), currently on Books tab, `BOOK001` is "Available" | 1. Locate book `BOOK001`. 2. Click the **+** (borrow) button. 3. Click **Borrow** on the confirmation dialog. | Book: `BOOK001` / Account: `binh.pham@email.com` | Borrowing is rejected. A specific error message appears: "Thành viên đã hết hạn. Không thể mượn sách." (or "Member is expired. Cannot borrow book."). Book status remains "Available". | REQ-04 | EP |
| TC-17 | Rejection - Limit Exceeded (Borrowing 4th book) | Logged in as Active Member (`ba.nguyen@email.com`), currently on Books tab, data in initial state (holds 1 book: `BOOK003` in seed data) | 1. Borrow two available books (e.g., `BOOK001` and `BOOK002`) by clicking **+** and confirming, reaching the limit of 3 books. 2. Locate a 4th available book (e.g., `BOOK005`). 3. Click the **+** (borrow) button next to `BOOK005`. 4. Click **Borrow** on the confirmation dialog. | Books: `BOOK001`, `BOOK002` (to reach limit), then `BOOK005` (4th book) / Account: `ba.nguyen@email.com` | Borrowing of `BOOK005` fails. A specific notification appears: "Đã đạt giới hạn mượn tối đa (3 sách)." (or "Maximum borrow limit reached (3 books)."). Book `BOOK005` status remains "Available". | REQ-04 | BVA |
| TC-18 | Successful Return - On-Time (No Overdue Alert) | Logged in as Active Member (`ba.nguyen@email.com`), currently has an active, on-time loan for `BOOK001` | 1. Switch to **Borrow/Return** tab. 2. Locate active record for `BOOK001` (within 14-day limit). 3. Click the **Return Book** button next to it. | Book: `BOOK001` / Account: `ba.nguyen@email.com` | Return is processed successfully. Notification "Book returned successfully." appears. The book's status in the list changes to "Returned" with current date. On the Books tab, `BOOK001` status immediately changes to "Available". No overdue alert is shown. | REQ-05 | EP |
| TC-19 | Successful Return - Overdue Book (Triggers Overdue Warning Alert) | Logged in as Active Member (`ba.nguyen@email.com`), has overdue seed loan record `BR001` | 1. Switch to **Borrow/Return** tab. 2. Locate record `BR001` (`BOOK003` - Overdue). 3. Click the **Return Book** button next to it. | Book: `BOOK003` / Account: `ba.nguyen@email.com` | Return is processed successfully. An **overdue warning alert** is displayed on the screen (e.g., warning that the book was returned late). The loan status updates to "Returned" with return date. On the Books tab, `BOOK003` immediately changes to "Available". | REQ-05 | EP, BVA |

---

## Summary

| Feature Group | TC Count | REQ Coverage | IDM Technique Applied |
|---------------|----------|--------------|----------------------|
| Login | 5 | REQ-01 | EP |
| View Book List | 6 | REQ-02 | EP |
| Borrow Books | 6 | REQ-04 | EP, BVA |
| Return Books | 2 | REQ-05 | EP, BVA |
| **Total** | **19** | REQ-01, REQ-02, REQ-04, REQ-05 | EP, BVA |
