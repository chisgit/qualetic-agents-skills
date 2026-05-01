# Skill: Documentation

Techniques for writing technical documentation that is accurate, concise, and useful to its intended audience.

## Documentation Principles

1. **Audience first** – Identify who will read this and tailor depth, vocabulary, and examples accordingly.
2. **One source of truth** – Documentation lives in one canonical place; everything else links to it.
3. **Accuracy over completeness** – A short accurate doc is better than a long inaccurate one.
4. **Progressive disclosure** – Lead with the simplest useful information; details come later.
5. **Show, don't just tell** – Examples are often clearer than prose descriptions.

## Document Types and When to Use Them

| Type | Use When |
|---|---|
| README | Introduce a project or module to someone new |
| API Reference | Describe every endpoint, parameter, and return value |
| Runbook / How-To | Walk through a specific operational or setup task |
| Architecture Overview | Explain system structure and key design decisions |
| Troubleshooting Guide | Help users diagnose and fix common problems |
| Changelog | Record what changed between releases |

## Writing Checklist

- [ ] The first paragraph answers: *What is this? Why does it exist? Who uses it?*
- [ ] Prerequisites and setup steps are listed before usage examples.
- [ ] Code samples are minimal, runnable, and correct.
- [ ] Every configuration option is documented with type, default, and allowed values.
- [ ] Error messages users may encounter are explained with resolution steps.
- [ ] Terminology is defined on first use and used consistently thereafter.
- [ ] Internal implementation details are excluded from user-facing docs.

## Writing Style

- Use active voice: "The function returns X" not "X is returned by the function."
- Use second person: "You can configure…" not "The user can configure…"
- Use present tense: "The endpoint accepts…" not "The endpoint will accept…"
- Break instructions into numbered steps, not a single run-on paragraph.
- Keep paragraphs to ≤ 5 sentences. Use bullet lists for enumerated items.

## Code Example Quality

```markdown
# Good: minimal, runnable, demonstrates the most common use case
result = client.get("/users/123")
print(result.name)  # → "Alice"

# Bad: full application boilerplate obscures the point being made
import os, sys, json
from client import Client
def main():
    c = Client(os.getenv("API_URL"))
    r = c.get("/users/123")
    print(json.dumps(r, indent=2))
if __name__ == "__main__":
    main()
```

## Context Usage Optimization

- When documenting code, load only public interfaces and function signatures — not the full implementation.
- Use summary comments at the top of long source files rather than reading every line.
- Reuse existing glossary terms from other project documentation to avoid contradiction.
