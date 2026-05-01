# Guideline: Quality Standards

Shared definitions of quality that apply to all output produced by agents in this repository. Use these as acceptance gates before considering any task complete.

---

## Definition of Done

A task is **Done** only when all of the following are true:

- [ ] The implementation satisfies all acceptance criteria.
- [ ] Unit tests cover all new logic (see [testing.md](../skills/testing.md) for coverage targets).
- [ ] The code builds and all tests pass in CI.
- [ ] The linter passes with no new warnings.
- [ ] No secrets, tokens, or credentials are present in source files.
- [ ] Any new public API, function, or configuration is documented.
- [ ] A code review has been completed and all `blocking` issues resolved.
- [ ] The PR description explains *what* changed and *why*.

---

## Code Quality Standards

### Correctness
- All code paths are tested, including error conditions.
- Edge cases (empty input, null/nil, maximum values) are handled explicitly.
- Errors are surfaced to callers; never silently swallowed.

### Readability
- Code reads like a series of clear, deliberate instructions.
- Variable and function names describe what they are/do, not how they work.
- Complex logic is accompanied by a comment explaining *why*, not *what*.
- Functions are ≤ 40 lines; nesting is ≤ 3 levels deep.

### Maintainability
- No duplication: shared logic is extracted into reusable utilities.
- No magic numbers or unexplained string literals.
- Dependencies are explicitly declared and pinned.
- Dead code is removed immediately, not commented out.

### Security
- User-supplied input is never trusted without validation.
- Authentication is required for every endpoint by default; exceptions are explicit.
- Secrets are managed via a secrets manager, never hardcoded.
- Dependencies are scanned for known vulnerabilities before adoption.

---

## Documentation Quality Standards

- Every public API, module, and configuration option is documented.
- All code examples in documentation are syntactically correct and tested.
- Documentation is updated in the same PR as the code change it describes.
- No "TBD", "coming soon", or "TODO" content is merged to main without a linked issue.

---

## Planning Quality Standards

- Every task has acceptance criteria verifiable without asking the author.
- Every task is independently completable without hidden pre-requisites.
- Risks and unknowns are surfaced as explicit items in the plan, not hidden.
- Estimates are relative (XS–XL) and agreed-upon before work begins.

---

## Review Quality Standards

- Every `blocking` review comment has a concrete, actionable suggestion.
- Reviews are completed within 24 hours of request.
- Reviews focus on the diff; do not expand scope to unrelated code.
- Approvals are not granted when security issues are unresolved.

---

## Continuous Improvement

When a defect, production incident, or missed requirement is discovered:

1. Write a regression test that would have caught it.
2. Document the root cause in a post-mortem or retrospective note.
3. Update these quality standards if a gap is identified.
