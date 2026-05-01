# Skill: Planning

Techniques for decomposing requirements into actionable tasks, estimating effort, and sequencing work for predictable delivery.

## Decomposition Strategy

Break work down from largest to smallest granularity:

```
Epic → Feature → User Story → Task → Sub-task
```

Stop decomposing when each item can be:
- Completed independently by a single agent or developer.
- Verified against clear acceptance criteria.
- Estimated with reasonable confidence.

## Writing Good User Stories

Use the format: **As a** `<role>`, **I want** `<capability>` **so that** `<benefit>`.

| Weak | Strong |
|---|---|
| "Add user auth" | "As a new visitor, I want to register with email and password so that I can access my saved content" |
| "Fix the dashboard" | "As an admin, I want the dashboard to load in under 2 seconds so that I can review reports efficiently" |

## Acceptance Criteria

Each story must have acceptance criteria that are:
- **Specific** – No room for interpretation.
- **Verifiable** – A reviewer can confirm pass/fail without asking the author.
- **Complete** – Cover happy path, error path, and edge cases.

Template:
```
Given <initial context>
When <action is taken>
Then <observable outcome>
```

## Estimation

Use relative sizing rather than hours to reduce bias:

| Size | Description |
|---|---|
| XS | Well-understood change to a single file, < 1 hour |
| S | Clear scope, 1–4 hours, minimal unknowns |
| M | Moderate complexity, half-day to 1 day |
| L | Complex or cross-cutting, 2–3 days |
| XL | Spike needed; break down before scheduling |

If a task is sized XL, it must be broken down further before work begins.

## Sequencing and Dependency Mapping

1. List all tasks.
2. For each task, identify any tasks it depends on.
3. Build a dependency graph and identify the critical path.
4. Schedule the critical path first to avoid bottlenecks.
5. Parallelize independent tasks.

## Risk Register

For each risk, capture:
- **Risk**: What could go wrong.
- **Probability**: Low / Medium / High.
- **Impact**: Low / Medium / High.
- **Mitigation**: How to reduce probability or impact.
- **Owner**: Who is monitoring this.

## Context Usage Optimization

- Work from requirement summaries, not raw meeting transcripts or full PRDs.
- Reference architecture overviews by section, not entire documents.
- Ask for clarification on the smallest ambiguous unit rather than loading more context.
