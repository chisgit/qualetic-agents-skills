# Code Review: [PR Title or Change Description]

> Replace all `[placeholder]` text with real values before use.

**PR / Change:** [Link or ID]  
**Author:** [Name or agent role]  
**Reviewer:** [Name or agent role]  
**Date:** [Date]  
**Verdict:** ✅ Approved | ⚠️ Approved with Comments | ❌ Changes Requested

---

## Summary

[1–3 sentence description of what this change does and why.]

---

## Review Checklist

### Correctness
- [ ] Implementation matches the stated requirements / acceptance criteria
- [ ] Edge cases and error paths are handled
- [ ] No off-by-one errors in loops or boundary conditions
- [ ] Concurrent access to shared state is safely handled (if applicable)

### Security
- [ ] User input is validated and sanitized
- [ ] No SQL injection, path traversal, or command injection vectors
- [ ] No hardcoded secrets, tokens, or credentials
- [ ] Authentication and authorization checks are present and correct
- [ ] Sensitive data is not logged or exposed in error messages

### Tests
- [ ] New functionality has corresponding tests
- [ ] Tests are independent and do not rely on execution order
- [ ] Tests cover at least one error/edge case per changed function
- [ ] All existing tests still pass

### Design
- [ ] Code follows the established architecture and patterns
- [ ] Functions are single-purpose and appropriately sized
- [ ] No unnecessary duplication introduced
- [ ] Public interfaces are documented

### Style
- [ ] Naming is clear and consistent with the codebase
- [ ] No dead code or commented-out blocks
- [ ] No magic numbers or unexplained literals

---

## Issues Found

> Format: `<File>:<Line> — <Severity>`  
> Severity: `blocking` | `recommended` | `nit`

### Issue 1

**Location:** `[file.py:42]` — `blocking`  
**Issue:** [What the problem is]  
**Suggestion:** [Concrete improvement with example if helpful]  
**Reason:** [Why this matters]

---

### Issue 2

**Location:** `[file.py:87]` — `recommended`  
**Issue:** [What the problem is]  
**Suggestion:** [Concrete improvement]  
**Reason:** [Why this matters]

---

### Issue 3

**Location:** `[file.py:101]` — `nit`  
**Issue:** [Minor style or readability issue]  
**Suggestion:** [Optional improvement]  
**Reason:** [Readability / consistency]

---

## Positive Observations

[Note 1–2 things done well. This reinforces good practices.]

- [Good pattern or decision worth calling out]
- [Another positive observation]

---

## Verdict

**Decision:** ✅ Approved | ⚠️ Approved with Comments | ❌ Changes Requested

**Required before merge:**
- [ ] [Blocking issue 1 must be resolved]
- [ ] [Blocking issue 2 must be resolved]

**Optional follow-up:**
- [ ] [Recommended improvement for a future PR]
