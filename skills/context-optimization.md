# Skill: Context Optimization

Strategies for maximizing the quality of agent output while minimizing the tokens consumed by the context window.

## Why Context Optimization Matters

- Larger contexts cost more tokens (time and money).
- Irrelevant context degrades output quality by distracting the model.
- Overly long prompts reduce precision — the model focuses less on what matters.
- Smaller, targeted contexts improve reproducibility and reliability of results.

## The Minimal Context Principle

> **Load only what is needed for this specific task. Nothing more.**

Before adding any file, document, or snippet to the context, ask:
- Will the model's output change if this is included? If no → exclude it.
- Is this the most current version? If no → update or exclude it.
- Can a summary replace the full content? If yes → summarize it.

## Context Loading Strategies

### 1. Interface over Implementation
When the agent needs to know what a module does (not how), provide:
- Function/method signatures with return types.
- Docstrings and comments.
- Public API contract.

Skip: internal logic, private functions, implementation details.

### 2. Diff over Full File
For code review or modification tasks:
- Provide the changed diff rather than the entire file.
- Only load the full file if the change requires understanding broader context.

### 3. Summary over Full Document
For large design documents or PRDs:
- Provide a 5–10 bullet summary of the key decisions.
- Link or reference the full document for lookup, but do not include it verbatim.

### 4. Relevant Section over Full File
For configuration files, large schemas, or long READMEs:
- Extract and include only the section relevant to the task.
- Note what was omitted so the agent doesn't assume it has the complete file.

## Context Budgeting

Allocate your token budget to the layers that matter most:

| Layer | Priority | Notes |
|---|---|---|
| System prompt / agent role | Highest | Keep concise; defines behaviour |
| Task description / acceptance criteria | High | Be precise; this drives the output |
| Directly modified code | High | Always include |
| Interfaces of dependencies | Medium | Include signatures; skip internals |
| Historical context / discussion | Low | Summarize only what changed decisions |
| Full files unchanged by the task | Exclude | Never include |

## Conversation and Session Management

- Start each new task with a fresh context when the prior task's state is not relevant.
- Summarize multi-turn conversations before continuing long chains.
- Use explicit markers to indicate what is still relevant: "Focus only on the items marked [ACTIVE]."
- Clear completed task artifacts from context before introducing new tasks.

## Prompt Efficiency Patterns

```markdown
# Inefficient: vague and overloaded
Review this entire codebase and tell me what needs to be improved.

# Efficient: specific, bounded, targeted
Review the diff in `src/auth/login.py` (attached) for security issues only.
Flag any input validation, authentication bypass, or secrets-handling concerns.
Output one issue per line as: <line>: <issue> | <severity>
```

| Pattern | Description |
|---|---|
| Constrain output format | Tell the agent exactly how to format output to avoid verbose responses |
| One task per call | Mixing multiple unrelated tasks in one prompt reduces quality for all |
| Specify what to ignore | "Do not review style; focus only on correctness" saves effort |
| Reference by name | "Use the pattern in `auth/middleware.py`" is more efficient than pasting it |

## Measuring Context Efficiency

After completing a task, ask:
- Was the output high quality despite the reduced context? If yes → further reduction may be possible.
- Did the model make incorrect assumptions? If yes → identify what was missing and add only that.
- Was any portion of the context never referenced in the output? If yes → it was waste; exclude it next time.
