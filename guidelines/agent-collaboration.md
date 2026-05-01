# Guideline: Agent Collaboration

How agents hand off work to each other, coordinate on shared tasks, and avoid duplication or conflict when multiple agents are active on the same project.

---

## Collaboration Model

Agents work in a **relay model**: each agent completes its stage, produces a well-defined output artifact, and hands off to the next agent. At no stage should two agents be modifying the same artifact simultaneously without explicit coordination.

```
Planner ──► Code Architect ──► Developer ──► Tester ──► Code Reviewer ──► Documentation Writer
   ▲                                            │              │
   └────────────────────────────────────────────┘              │
              (feedback loop for defects)                       │
   ◄───────────────────────────────────────────────────────────┘
              (feedback loop for review changes)
```

---

## Handoff Protocol

Each handoff must include:

1. **Output artifact**: The completed deliverable (code, plan, design document, etc.).
2. **Summary of decisions**: Key choices made and the rationale (prevents re-litigating resolved questions).
3. **Open items**: Anything unresolved that the next agent must address.
4. **Context pointer**: References to the minimum context needed for the next agent to continue.

### Example Handoff from Developer to Tester

```markdown
## Handoff: TASK-042 — User Login Implementation

**Artifact:** `src/auth/login.py` (see PR #42)

**Decisions Made:**
- Used bcrypt with cost factor 12 for password hashing.
- JWT expiry set to 15 minutes; refresh token to 7 days.
- Invalid credentials always return 401 (no user-enumeration distinction).

**Open Items:**
- Concurrent login session limiting is not implemented (TASK-055).
- Rate limiting for failed attempts is not in scope for this task.

**Context for Tester:**
- See `src/auth/login.py` and `src/auth/models.py` (interfaces only needed).
- Test framework: pytest, fixtures in `tests/conftest.py`.
- Acceptance criteria: TASK-042 in `templates/project-plan.md`.
```

---

## Conflict Resolution

If two agents reach different conclusions on the same decision:

1. The **Code Architect** is the tie-breaker for structural and technology decisions.
2. The **Code Reviewer** is the tie-breaker for coding standards decisions.
3. Escalate to a human stakeholder only when agents cannot resolve through the above.
4. Document the resolution as an ADR so it is not revisited unnecessarily.

---

## Avoiding Duplication

- Before starting work, each agent checks whether the artifact already exists or is being produced by another agent.
- Agents reference existing artifacts by path or link rather than reproducing their content.
- Skills and guidelines from this repository should be referenced by name, not copied inline into prompts.

---

## Context Handoff Efficiency

When passing context between agents:

- Pass the **output artifact and a brief summary**, not the entire prior conversation.
- Summarize decisions into bullet points; drop the deliberation that led to them.
- Reference files by path; load content only when the receiving agent must modify it.
- Explicitly state what the next agent should **not** re-do (prevents wasted effort).

---

## Feedback Loops

**Developer ← Tester**: When a defect is found during testing, the Tester returns:
- The failing test and the exact behavior observed.
- The acceptance criterion that is violated.
- *Not* a suggested fix — the Developer determines the fix.

**Developer ← Code Reviewer**: When changes are requested, the Reviewer returns:
- Specific `blocking` and `recommended` items only.
- Enough context per issue for the Developer to act without re-reading the full review.

**Planner ← Any Agent**: When scope, requirements, or estimates need to change, the affected agent returns:
- The specific task or story that needs updating.
- The new information that changes the plan.
- *Not* a full re-plan — the Planner determines the adjustment.
