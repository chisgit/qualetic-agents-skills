# Skill: Code Review

A systematic approach to reviewing code changes that balances thoroughness with efficiency.

## Review Mindset

- Review the *code*, not the author.
- Your goal is to ship better software, not to find fault.
- Ask questions when unclear; assume positive intent.
- Prioritize blocking issues over style preferences.

## Review Sequence

Work through the diff in this order to avoid missing issues:

1. **Understand intent** – Read the task description and acceptance criteria before looking at any code.
2. **Security pass** – Look specifically for vulnerabilities before anything else.
3. **Correctness pass** – Verify the logic is right for all expected and edge case inputs.
4. **Test coverage pass** – Check that the behavior being changed is adequately tested.
5. **Design pass** – Evaluate structure, naming, and alignment with architecture.
6. **Style pass** – Only after the above; flag style issues as `nit`, not blockers.

## Security Checklist

- [ ] User-supplied input is validated and sanitized before use.
- [ ] No SQL, OS command, or path injection vulnerabilities.
- [ ] Authentication and authorization checks are present and correct.
- [ ] No secrets, tokens, or credentials appear in code or logs.
- [ ] Dependencies are pinned and not known-vulnerable.
- [ ] Sensitive data is not logged or exposed in error messages.
- [ ] Cryptographic operations use well-known library functions (no home-grown crypto).

## Correctness Checklist

- [ ] Logic handles empty inputs, null/nil values, and boundary conditions.
- [ ] Off-by-one errors checked in loops and range operations.
- [ ] Concurrent access to shared state is properly synchronized.
- [ ] Resource cleanup is guaranteed (connections, file handles, locks).
- [ ] Error return values are checked at every call site.

## Test Coverage Checklist

- [ ] Every acceptance criterion has a corresponding test.
- [ ] Happy path is covered.
- [ ] At least one error/edge case per function is covered.
- [ ] Tests are independent and do not rely on test execution order.

## Feedback Format

Structure every comment as:

```
**Issue:** <what the problem is>
**Suggestion:** <concrete improvement>
**Reason:** <why it matters>
```

Label severity: `blocking` | `recommended` | `nit`

## Context Usage Optimization

- Review only the diff and files it directly touches.
- Do not pull in the full repo to provide context for a single changed function.
- Summarize patterns observed across the diff rather than re-reading unchanged code.

## When to Approve

Approve when:
- All `blocking` issues are resolved or have an agreed-upon plan.
- Test coverage is adequate for the risk level of the change.
- No unresolved security concerns remain.

Do not block on `nit` or `recommended` items — leave them for the author's discretion.
