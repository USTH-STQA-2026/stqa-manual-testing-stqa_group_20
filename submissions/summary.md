# Test Summary

> **Instructions**: This is a **Quality Assurance** activity — you are evaluating the overall quality of the software, not just listing bugs.

---

## 1. Group Information

| Item | Information |
|-----|----------|
| **Group** | `Group 20` |
| **Class** | `ICT.1` |
| **Report Date** | `25/05/2026` |

## 2. Overview of Results

| Metric | Value |
|--------|---------|
| Total test cases | 19 |
| Pass | 16 |
| Fail | 3 |
| Blocked | 0 |
| Not Run | 0 |
| **Pass Rate** | 84.2% |
| **Number of bugs found** | 4 |

### Distribution by Feature Group

| Feature Group | TC | Pass | Fail | Bug | Assessment |
|---------------|-----|------|------|-----|---------|
| Login (REQ-01) | 5 | 5 | 0 | 0 | Fully stable and returns correct error messages in all input scenarios. |
| View Book List (REQ-02) | 6 | 6 | 0 | 0 | Intuitive display interface, accurate real-time sync of book status after borrowing/returning. |
| Borrow Books (REQ-04) | 6 | 4 | 2 | 2 | Critical logic bug allows borrowing beyond the 3-book limit and displays incorrect error messages for suspended members. |
| Return Books (REQ-05) | 2 | 1 | 1 | 1 | Book return works normally, but when returning overdue books, the system fails to display any overdue warnings. |

### Bug Distribution by Severity

| Severity | Quantity | Bug IDs |
|--------|---------|---------|
| High | 1 | BUG-02 (Allows borrowing the 4th book) |
| Medium | 3 | BUG-01 (Librarian lacks button to borrow on behalf of members), BUG-03 (Overdue return warning not displayed), BUG-04 (Incorrect error message for suspended members) |
| Low | 0 | — |

---

## 3. Test Design Techniques Applied

| Technique | Applied to which REQ? | Number of TCs Used | Explanation of Application |
|----------|---------------------|---------------|------------------------|
| EP (Equivalence Partitioning) | REQ-01, REQ-02, REQ-04, REQ-05 | 17 | Partitioning inputs into valid/invalid equivalence classes (e.g., book status, account roles, member status). |
| BVA (Boundary Value Analysis) | REQ-04, REQ-05 | 3 | Testing at critical boundary values (e.g., attempting to borrow a 4th book when the limit of 3 books is reached in TC-17; boundary timing of on-time vs. overdue returns in TC-19). |

---

## 4. Software Quality Analysis

### 4.1. Strengths
- User-friendly, easy-to-use interface, extremely fast response time due to in-memory data storage.
- Real-time synchronization of book status between the **Books** tab and the **Borrow/Return** tab without requiring a page refresh.
- Clear role-based authorization for login between Librarian and Member roles.

### 4.2. Weaknesses
- Critical logic error in enforcing the maximum borrow limit for Members (BUG-02).
- Mismatched and incorrect error message response for suspended Members (BUG-04).
- The system completely ignores displaying an overdue warning when a Member returns a book late (BUG-03).
- Discrepancy between SRS and UI, as the Librarian role lacks the option to borrow books on behalf of other Members (BUG-01).

---

## 5. Bug Fixing Priority Recommendations

| Priority | Bug | Severity | Reason for Priority |
|--------|-----|--------|---------------|
| 1 | BUG-02 (Borrowing exceeds the 3-book limit) | High | This is the most critical business logic flaw, risking library book assets and directly violating a core business rule. |
| 2 | BUG-04 (Incorrect error message for suspended members) | Medium | Causes significant confusion to users and impacts support service experience (suspended account is reported as expired). |
| 3 | BUG-03 (Fails to display overdue return warning) | Medium | Violates business feedback rules specified in REQ-05 for members returning books past their due dates. |
| 4 | BUG-01 (Librarian lacks borrow-on-behalf button) | Medium | Missing part of the standard workflow of Librarians described in the SRS, UI needs enhancement. |

---

## 6. Conclusion

**The system is NOT READY FOR RELEASE**. Although the interface and basic borrow/return flow work smoothly, critical business logic bugs (BUG-02) and missing/incorrect business warning alerts (BUG-03, BUG-04) are major blockages. BUG-02 and BUG-03 must be resolved immediately before the system can be deployed in production.

---

## 7. Lessons Learned (Optional)

`<!-- What did your group learn from this testing process? -->`

---

## 8. AI Usage Declaration (Optional)

> If the group used AI tools (ChatGPT, Copilot, Gemini...), please declare them below. Honest declarations **do not affect grades** — this is a transparency skill in the industry.

| AI Tool | Component Used For | How You Checked/Edited |
|------------|-------------------|-----------------------------------|
| Claude | Documentation | Analyzed and summarized documentation, searched for specific terms in documents faster. |
