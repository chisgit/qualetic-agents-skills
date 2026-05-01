# Guideline: Tokenization Optimization

Practical techniques for reducing token consumption while maintaining — or improving — output quality.

---

## Why This Matters

Every token in the context window has a cost:

- **Latency**: More tokens → slower responses.
- **Financial cost**: Most LLM APIs charge per token.
- **Quality**: Models attend less precisely to important content when surrounded by noise.
- **Limits**: Context windows are finite; inefficient use means hitting limits prematurely.

The goal is **signal density**: maximize the useful information per token.

---

## Prompt Engineering for Efficiency

### Be Explicit About Output Format

Vague prompts produce verbose, exploratory responses. Precise format instructions eliminate preamble and post-amble.

| Inefficient | Efficient |
|---|---|
| "Explain what this code does" | "List the 3 main responsibilities of this function in bullet points, each ≤ 10 words" |
| "Review this PR" | "List only `blocking` security issues. Format: `file:line — issue — suggestion`" |
| "Write a plan for this feature" | "Produce 5 tasks using the TASK format in `templates/project-plan.md`" |

### Scope Instructions Tightly

```markdown
# Wastes tokens:
Review this entire codebase for improvements.

# Efficient:
Review only `src/auth/login.py` lines 40–80 for input validation issues.
```

### Eliminate Soft Preamble

Avoid openers that consume tokens without adding information:
- ❌ "Certainly! I'd be happy to help with that..."
- ❌ "Great question! Let me think through this..."
- ✅ Start directly with the output.

Add this to system prompts: *"Begin responses directly with the requested output. No preamble."*

---

## Input Context Efficiency

### Token Density Comparison

| Input Type | Approximate Token Cost | Use When |
|---|---|---|
| Full source file (500 lines) | ~2000–4000 tokens | Must edit file directly |
| Function signatures only | ~100–300 tokens | Need to understand interface |
| Diff only | ~200–800 tokens | Reviewing or small modification |
| 5-bullet summary of a doc | ~100–150 tokens | Need to reference a decision |
| Full design document (2000 words) | ~2500–3000 tokens | Almost never |

### File Loading Decision Tree

```
Do I need to READ and UNDERSTAND this file?
  └── Yes → Do I need the full file or just its interface?
              ├── Interface only → Load signatures + docstrings only
              └── Full file needed → Load it
  └── No → Do I need to REFERENCE a decision from it?
              ├── Yes → Summarize in 3–5 bullets; don't load the file
              └── No → Exclude it entirely
```

---

## Structured Output Patterns

Use structured formats that compress information:

```markdown
# Instead of:
"The function on line 42 has a problem where it doesn't handle the case
when the input is None, which could cause a NullPointerException when
the code tries to access the .name property of the object."

# Use:
`login.py:42` — blocking — input not validated for None; add `if user is None: raise ValueError`
```

### Preferred Compact Formats

| Task | Compact Format |
|---|---|
| Code issues | `file:line — severity — issue — fix` |
| Task list | `TASK-NNN: title [estimate] [dependency]` |
| Decision log | `ADR-NNN: title — decision — trade-off` |
| Status update | `[done] [in-progress] [blocked] task-title — blocker if applicable` |

---

## Conversation and Session Management

- **Summarize before extending**: If a conversation has exceeded ~10 turns, summarize the decisions made so far and start a new session with that summary as context.
- **Checkpoint frequently**: After each agent completes a stage, save the output artifact. The artifact (not the conversation) becomes the handoff.
- **Prune resolved items**: Remove completed tasks, resolved issues, and answered questions from active context.
- **One task per session**: Mixing multiple unrelated tasks in one context degrades quality for all of them.

---

## Model Selection for Cost Efficiency

Match model capability to task complexity:

| Task Type | Recommended Model Tier |
|---|---|
| Boilerplate code generation, simple transforms | Smaller / faster model |
| Complex architecture decisions, nuanced review | Larger / more capable model |
| Summarization and formatting | Smaller / faster model |
| Security analysis, edge case reasoning | Larger / more capable model |

Do not use the most powerful (and expensive) model for every task. Reserve it for tasks that genuinely require deep reasoning.

---

## Measuring and Improving

Track these signals to continuously improve token efficiency:

1. **Output quality per token**: Did the response directly answer the question? If padded with caveats and repetition, tighten the prompt.
2. **Context utilization**: What percentage of the loaded context was actually referenced in the output? Unused context is waste.
3. **Re-work rate**: How often does an agent produce output that requires a follow-up correction? Clearer prompts and format instructions reduce this.
4. **Session length**: Sessions that extend beyond ~20 turns typically suffer from context degradation. Summarize and reset.
