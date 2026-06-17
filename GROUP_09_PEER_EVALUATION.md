# PEER EVALUATION REPORT — GROUP 09

**FROM:** Group 20 (Evaluator)
https://github.com/USTH-STQA-2026/stqa-manual-testing-stqa_group_20

---

## SUMMARY

31 test cases cover all 8 REQs and use EP, BVA, DT, and IDM. The group found 10 real bugs, each checked against the SRS and backed by evidence. Coverage and test design are good. The weak spots: REQ-02 and REQ-08 have too few tests, BVA tests only one value, and one decision-table row uses a status that is not in the SRS.

---

## RATING USING RUBRIC

| # | Criterion | Wt | Band | Score |
|---|---|---|---|---|
| 1 | Functional coverage | 25% | Good-Excellent | 8.5 |
| 2 | Design techniques | 25% | Good | 8.0 |
| 3 | Description quality | 20% | Good | 7.5 |
| 4 | Bug reporting | 20% | Good | 7.0 |
| 5 | Presentation & format | 10% | Pass-Good | 6.0 |
| | **BASE** | | | **7.6** |
| | **FINAL (+1.5 bonus)** | | | **9.1** |

---

## GOOD POINTS

- 31 test cases, all 8 REQs, with happy, negative, and boundary tests. More than the minimum and the bonus target.
- Uses EP, BVA, and DT, and says why each was chosen. The IDM step is extra work beyond what was asked.
- Found 10 real bugs, all checked against the SRS, all with proof (including video). The severity ratings make sense.
- Earned all four bonus points (B1-B4): 31 tests, a Borrow decision table, proof for every bug, and a fix-order list.

## WEAK POINTS

1. **TOO FEW TESTS IN SOME AREAS.** REQ-02 has 2 tests and REQ-08 has 1. Boundary tests only check the 3-book limit.
2. **TECHNIQUE GAPS.** BVA tests only one value. The Borrow decision table row R3 uses a "Lost" status that is not in the SRS — add a source or remove it.
