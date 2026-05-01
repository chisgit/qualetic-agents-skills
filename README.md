# qualetic-agents-skills

A curated collection of standardized agent definitions, skills, templates, and guidelines designed to make Agentic AI efficient and effective. Any agentic harness can reference these files to produce high-quality applications, documentation, and plans with optimized use of context and tokenization.

## Purpose

This repository provides **reusable building blocks** that any AI agent or orchestration framework can adopt:

- **Agents** – Specialized roles with defined responsibilities, context requirements, and output expectations.
- **Skills** – Discrete, composable capabilities that agents can apply to accomplish tasks.
- **Templates** – Standardized output structures for applications, documentation, plans, and reviews.
- **Guidelines** – Cross-cutting best practices for quality, collaboration, and token efficiency.

## Repository Structure

```
qualetic-agents-skills/
├── agents/                    # Specialized agent role definitions
│   ├── code-architect.md      # High-level design and architecture decisions
│   ├── developer.md           # Feature implementation and coding
│   ├── code-reviewer.md       # Code quality, security, and performance review
│   ├── documentation-writer.md# Technical writing and documentation
│   ├── planner.md             # Project planning and task decomposition
│   └── tester.md              # Test strategy and test implementation
│
├── skills/                    # Reusable capabilities for agents
│   ├── code-generation.md     # Best practices for generating clean code
│   ├── code-review.md         # Systematic review techniques
│   ├── documentation.md       # Writing effective technical documentation
│   ├── testing.md             # Testing methodologies and strategies
│   ├── planning.md            # Estimation, decomposition, and sequencing
│   └── context-optimization.md# Minimizing context window usage
│
├── templates/                 # Standardized output templates
│   ├── new-application.md     # Scaffold for starting a new project
│   ├── project-plan.md        # Structured project plan
│   ├── documentation.md       # Documentation template
│   └── code-review.md         # Code review report template
│
└── guidelines/                # Cross-cutting standards and practices
    ├── quality-standards.md   # Definitions of done and quality gates
    ├── agent-collaboration.md # How agents hand off and coordinate
    └── tokenization-optimization.md # Reducing token cost without losing quality
```

## How to Use

1. **Reference an agent definition** when configuring a role in your agentic harness.
2. **Attach relevant skills** to that agent so it knows *how* to perform its tasks.
3. **Use a template** as the starting scaffold for its expected output.
4. **Apply the guidelines** to keep quality high and context usage lean.

Each file is self-contained and written in plain Markdown so it can be injected directly into a system prompt, attached as a file reference, or read by a retrieval-augmented generation (RAG) pipeline.

## Contributing

Add new agent definitions, skills, templates, or guidelines following the conventions already established in each directory. Keep files focused, concise, and free of implementation-specific details so they remain reusable across projects and tech stacks.
