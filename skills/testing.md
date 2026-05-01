# Skill: Testing

Strategies and patterns for writing tests that are reliable, readable, and fast.

## Testing Pyramid

Structure the test suite so the bulk of tests are fast and isolated:

```
        /\
       /  \          E2E Tests (few, slow, high confidence)
      /----\
     /      \        Integration Tests (moderate, some coupling)
    /--------\
   /          \      Unit Tests (many, fast, isolated)
  /____________\
```

- **Unit tests**: Test a single function or class in isolation. Mock all external dependencies.
- **Integration tests**: Test two or more real components interacting (e.g., service + database).
- **End-to-end tests**: Test the full user journey through the actual system.

## Test Structure: Arrange-Act-Assert

Every test should follow AAA:

```python
def test_calculate_total_with_discount():
    # Arrange
    cart = Cart(items=[Item(price=100), Item(price=50)])
    discount = PercentageDiscount(rate=0.10)

    # Act
    total = calculate_total(cart, discount)

    # Assert
    assert total == 135.0
```

## Naming Tests

Use descriptive names that communicate *what* is being tested and *under what condition*:

```
should_<expected behavior>_when_<condition>
calculate_total_returns_discounted_price_when_discount_applied
login_fails_when_password_is_empty
```

## What to Test

Prioritize tests for:
1. Public API boundaries (functions, endpoints, events).
2. Business rules and domain logic.
3. Error handling and failure modes.
4. Security-sensitive code paths.
5. Previously reported defects (regression tests).

De-prioritize:
- Trivial getters/setters with no logic.
- Third-party library behavior (trust the library's own tests).
- Implementation internals that are likely to change.

## Test Isolation Checklist

- [ ] Test does not depend on execution order (no shared mutable state).
- [ ] Test sets up all data it needs in its own Arrange section.
- [ ] Test tears down or resets any state it creates.
- [ ] Time-sensitive tests use fake clocks, not `sleep`.
- [ ] Network and I/O calls are mocked or use test doubles.

## Coverage Targets

| Code Type | Minimum Coverage |
|---|---|
| Business logic / domain rules | 90% |
| API handlers / controllers | 80% |
| Infrastructure / adapters | 70% |
| Configuration and wiring | Integration tested |

Coverage % is a signal, not a goal — 100% coverage with bad assertions is worse than 70% with precise assertions.

## Context Usage Optimization

- Load only the public interface of the module under test — not its full implementation.
- Reuse existing test helpers and fixtures rather than recreating them inline.
- When adding tests for a bug fix, load only the failing test and the code path it exercises.
