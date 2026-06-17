# Test Summary

> **Instructions**: This is a **Quality Assurance** activity — you are evaluating the overall quality of the software, not just listing bugs.

---

## 1. Group Information

| Item | Information |
|-----|----------|
| **Group** | `Group 20` |
| **Class** | `ICT.1` |
| **Report Date** | `30/05/2026` |

## 2. Overview of Results

| Metric | Value |
|--------|-------|
| Total test cases | 34 |
| Pass | 27 |
| Fail | 7 |
| Blocked | 0 |
| Not Run | 0 |
| **Pass Rate** | **79.4%** |
| **Number of bugs found** | 8 |

### Distribution by Feature Group

| Feature Group | TC | Pass | Fail | Bug | Assessment |
|---------------|-----|------|------|-----|---------|
| Login (REQ-01) | 5 | 5 | 0 | 0 | Fully stable and returns correct error messages in all input scenarios. |
| View Book List (REQ-02) | 6 | 6 | 0 | 0 | Intuitive display interface, accurate real-time sync of book status after borrowing/returning. |
| Search & Filter (REQ-03) | 6 | 5 | 1 | 1 | Basic search works, but combination logic (AND) between Search and Genre filter is broken. |
| Borrow Books (REQ-04) | 6 | 4 | 2 | 2 | Critical logic bug allows borrowing beyond the 3-book limit and displays incorrect error messages for suspended members. |
| Return Books (REQ-05) | 2 | 1 | 1 | 1 | Book return works normally, but when returning overdue books, the system fails to display any overdue warnings. |
| Overdue Processing (REQ-06) | 2 | 2 | 0 | 0 | Manual scan for overdue books updates statuses correctly in both Librarian and Member views. |
| Member Management (REQ-07) | 4 | 2 | 2 | 2 | Only Librarian can access. Creation works but critical email syntax validation bypass allows invalid emails (BUG-06), and duplicate emails return incorrect generic error messages (BUG-07). |
| Borrow Record Lookup (REQ-08) | 3 | 2 | 1 | 1 | Librarian can see all records, and Member can see personal records. However, a critical security vulnerability allows Members to query other members' records (BUG-08). |

### Bug Distribution by Severity

| Severity | Quantity | Bug IDs |
|--------|---------|---------|
| High | 4 | BUG-02 (Allows borrowing the 4th book), BUG-05 (Search and filter logic failure), BUG-06 (Bypasses email syntax check), BUG-08 (Security data leak: member can view others' records) |
| Medium | 4 | BUG-01 (Librarian lacks button to borrow on behalf of members), BUG-03 (Overdue return warning not displayed), BUG-04 (Incorrect error message for suspended members), BUG-07 (Incorrect error message for duplicate email) |
| Low | 0 | — |

---

## 3. Test Design Techniques Applied

| Technique | Applied to which REQ? | Number of TCs Used | Explanation of Application |
|----------|---------------------|---------------|------------------------|
| EP (Equivalence Partitioning) | REQ-01, REQ-02, REQ-03, REQ-04, REQ-05, REQ-06, REQ-07, REQ-08 | 31 | Partitioning inputs into valid/invalid equivalence classes (e.g., book status, account roles, search keywords, member status, email format, record authorization). |
| BVA (Boundary Value Analysis) | REQ-03, REQ-04, REQ-05 | 3 | Testing at critical boundary values (e.g., 100% exact title match in TC-16; attempting to borrow a 4th book when the limit of 3 is reached in TC-23). |

---

## 4. Software Quality Analysis

### 4.1. Strengths
- User-friendly, easy-to-use interface, extremely fast response time due to in-memory data storage.
- Real-time synchronization of book status between the **Books** tab and the **Borrow/Return** tab without requiring a page refresh.
- Clear role-based authorization for login between Librarian and Member roles.
- Restricts general tab view for Member accounts, preventing direct access to the administrative Members tab.

### 4.2. Weaknesses
- **Critical security vulnerability (Data Leak)**: Member role can look up and spy on any other member's borrowing history just by guessing their ID (BUG-08).
- Critical logic error in enforcing the maximum borrow limit for Members (BUG-02).
- Broken email syntax validation: allows adding a member with an invalid email address (BUG-06).
- Broken AND logic for search and genre filter (BUG-05), where genre overrides keyword.
- Mismatched and incorrect error message response for suspended Members (BUG-04) and duplicate email creation (BUG-07).
- The system completely ignores displaying an overdue warning when a Member returns a book late (BUG-03).
- Discrepancy between SRS and UI, as the Librarian role lacks the option to borrow books on behalf of other Members (BUG-01).

---

## 5. Bug Fixing Priority Recommendations

| Priority | Bug | Severity | Reason for Priority |
|--------|-----|--------|---------------|
| 1 | BUG-08 (Security data leak of borrow records) | High | This is a critical security vulnerability where user privacy data is leaked. Any member can spy on other members' reading history, violating basic compliance rules. |
| 2 | BUG-02 (Borrowing exceeds the 3-book limit) | High | This is a major business logic flaw, risking library book assets and directly violating a core business rule. |
| 3 | BUG-06 (Bypasses email syntax validation) | High | Allows invalid email data into the in-memory database, leading to potential data corruption. |
| 4 | BUG-05 (Search AND Filter logic failure) | High | Prevents users from effectively finding specific books within categories, impacting core usability. |
| 5 | BUG-04 (Incorrect error message for suspended members) | Medium | Causes significant confusion to users and impacts support service experience. |
| 6 | BUG-07 (Incorrect error message for duplicate email) | Medium | Confuses the administrator, making them believe they wrote an invalid email instead of showing the email is a duplicate. |
| 7 | BUG-03 (Fails to display overdue return warning) | Medium | Violates business feedback rules specified in REQ-05. |
| 8 | BUG-01 (Librarian lacks borrow-on-behalf button) | Medium | UI enhancement needed to align with the standard workflow described in the SRS. |

---

## 6. Conclusion

**The system is NOT READY FOR RELEASE**. Although the interface and basic flows work smoothly, multiple critical security vulnerabilities (BUG-08), business logic bugs (BUG-02, BUG-05, BUG-06) and missing warning alerts (BUG-03, BUG-04, BUG-07) are major blockages. BUG-08, BUG-02, and BUG-06 must be resolved immediately before the system can be considered for production.

---

## 7. Lessons Learned (Optional)
- The importance of security testing even for client-side applications. Restricting UI tabs (e.g. hiding the Members tab) does not guarantee that other endpoints or views (like the Lookup search) are secure.
- The importance of verifying combination logic (Search + Filter) as individual features might work while their intersection fails.
- Role-based testing is crucial to ensure Librarians have all required administrative tools.
- Real-time UI updates require careful state management to ensure consistency across different tabs.

---

## 8. AI Usage Declaration (Optional)

> If the group used AI tools (ChatGPT, Copilot, Gemini...), please declare them below. Honest declarations **do not affect grades** — this is a transparency skill in the industry.

| AI Tool | Component Used For | How You Checked/Edited |
|------------|-------------------|-----------------------------------|
| Claude | Documentation | Analyzed and summarized documentation, searched for specific terms in documents faster. |
| Gemini | Content Migration & Refinement | Migrated and translated test cases/results from temp files to English, renumbered and aligned TC sequence, and synchronized all summary metrics across the submission files. |
| Antigravity AI |  Verification | Verify validations, and capture evidence screenshots. |
| Claude | Submission refinement | Fixed cross-document inconsistencies (malformed TC reference in BUG-01, a mismatched actual-result entry, bug-section ordering) and renumbered all test cases into a single contiguous sequence grouped by REQ, renaming evidence screenshots to match. All test results and findings are the team's own; no results were altered. |
