# Skill: Code Generation

Guidance for producing clean, correct, and maintainable code in any language or framework.

## Core Principles

1. **Correctness first** – Code must do what it is supposed to do before any other optimization.
2. **Readability over cleverness** – A future reader (human or agent) should understand intent immediately.
3. **Fail loudly** – Surface errors explicitly; never hide failures behind empty catches or silent fallbacks.
4. **Minimal surface area** – Only expose what callers need; keep everything else private or internal.
5. **Consistency** – Match the style, naming, and patterns already in the codebase.

## Before Writing Code

- Re-read the acceptance criteria. Write tests for them first if the project uses TDD.
- Identify which existing modules, utilities, or patterns to reuse.
- Clarify any ambiguities in the requirements *before* generating code.

## Naming Conventions

| Element | Convention |
|---|---|
| Variables and functions | Descriptive, lowercase with underscores (Python/Go) or camelCase (JS/TS/Java) |
| Constants | `UPPER_SNAKE_CASE` |
| Classes/types | `PascalCase` |
| Boolean variables | Prefix with `is`, `has`, `can`, `should` |
| Functions | Start with a verb — `get`, `fetch`, `calculate`, `validate`, `create` |

## Structuring Code

- **Single responsibility**: Each function does one thing.
- **Max function length**: Aim for ≤ 40 lines. Longer functions usually hide multiple responsibilities.
- **Depth limit**: Aim for ≤ 3 levels of nesting. Refactor deeply nested logic with early returns or extracted helpers.
- **Parameter count**: ≤ 4 parameters per function. Use an options object/struct for more.

## Error Handling

```
# Pattern: always handle errors at the call site
result, err = do_something()
if err != None:
    return None, wrap_error("context about what failed", err)
```

- Return errors to callers; do not silently swallow them.
- Add context when wrapping errors (what operation failed, with what inputs).
- Distinguish between recoverable errors (return error) and programmer errors (panic/assert).

## Context Usage Optimization

- Load only the files being modified and their direct dependencies.
- Do not load test files when generating production code (and vice versa).
- Summarize long files rather than loading them entirely if only the interface is needed.
- Stop generation as soon as the task is complete; do not generate speculative future code.

## Checklist Before Finalizing

- [ ] Compiles/parses without errors or warnings.
- [ ] No hardcoded secrets, magic numbers, or environment-specific strings.
- [ ] All public functions and types have documentation comments.
- [ ] Error paths handled; no empty catch blocks.
- [ ] Matches existing style (indentation, quotes, brackets).
- [ ] No dead code or commented-out blocks.
