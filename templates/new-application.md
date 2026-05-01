# New Application: [Project Name]

> Replace all `[placeholder]` text with real values before use.

## Overview

**Project Name:** [Name]  
**Summary:** [One-paragraph description of what the application does and the problem it solves]  
**Primary Users:** [Who will use this]  
**Stakeholder / Owner:** [Name or team]  
**Target Completion:** [Date or milestone]

---

## Problem Statement

[Describe the current pain point or gap. What is broken, missing, or inefficient today? Keep to 3–5 sentences.]

---

## Goals and Non-Goals

### Goals
- [ ] [Measurable outcome 1, e.g., "Reduce order processing time from 10 minutes to 30 seconds"]
- [ ] [Measurable outcome 2]
- [ ] [Measurable outcome 3]

### Non-Goals (explicitly out of scope)
- [Excluded feature or concern 1]
- [Excluded feature or concern 2]

---

## Requirements

### Functional Requirements
| ID | Requirement | Priority |
|---|---|---|
| FR-001 | [Requirement description] | Must Have |
| FR-002 | [Requirement description] | Should Have |
| FR-003 | [Requirement description] | Nice to Have |

### Non-Functional Requirements
| ID | Requirement | Target |
|---|---|---|
| NFR-001 | Response time (P95) | < 500ms |
| NFR-002 | Availability | 99.9% |
| NFR-003 | Concurrent users | [number] |
| NFR-004 | Data retention | [duration] |

---

## Architecture Overview

### System Components

```
[ASCII or Mermaid diagram of main components and their relationships]

Example:
  [Browser]
     │ HTTPS
  [API Gateway]
     │ ├── [Auth Service]
     │ └── [Core Service]
              │
           [Database]
```

### Technology Stack

| Layer | Technology | Rationale |
|---|---|---|
| Frontend | [e.g., React, Vue, None] | [Why] |
| Backend | [e.g., Python/FastAPI, Go, Node] | [Why] |
| Database | [e.g., PostgreSQL, DynamoDB] | [Why] |
| Infrastructure | [e.g., AWS, GCP, Docker + k8s] | [Why] |
| Auth | [e.g., OAuth 2.0 / JWT, Auth0] | [Why] |
| Observability | [e.g., Prometheus + Grafana, Datadog] | [Why] |

### Key Architecture Decisions

1. **[Decision title]**: [What was decided and why. Trade-offs acknowledged.]
2. **[Decision title]**: [What was decided and why. Trade-offs acknowledged.]

---

## Data Model

### Core Entities

```
[Entity name]
  - id: UUID
  - [field]: [type]
  - created_at: timestamp
  - updated_at: timestamp

[Entity name]
  - id: UUID
  - [field]: [type]
```

### Relationships

- [Entity A] has many [Entity B]
- [Entity B] belongs to [Entity A]

---

## API Design (if applicable)

| Method | Path | Description | Auth Required |
|---|---|---|---|
| GET | `/api/v1/[resource]` | List all [resources] | Yes |
| POST | `/api/v1/[resource]` | Create a new [resource] | Yes |
| GET | `/api/v1/[resource]/{id}` | Get a specific [resource] | Yes |
| PUT | `/api/v1/[resource]/{id}` | Update a [resource] | Yes |
| DELETE | `/api/v1/[resource]/{id}` | Delete a [resource] | Yes |

---

## Security Considerations

- [ ] Authentication mechanism defined: [describe]
- [ ] Authorization / RBAC model defined: [describe]
- [ ] Sensitive data encrypted at rest: [yes/no, which fields]
- [ ] Sensitive data encrypted in transit: [TLS version]
- [ ] Input validation strategy: [describe]
- [ ] Rate limiting: [yes/no, limits]
- [ ] Secrets management: [e.g., Vault, AWS Secrets Manager, env vars via CI]

---

## Project Plan

See [`templates/project-plan.md`](project-plan.md) for the task breakdown.

**Milestones:**

| Milestone | Target Date | Definition of Done |
|---|---|---|
| M1: Foundation | [date] | Repo, CI/CD, dev environment working |
| M2: Core Feature | [date] | [Core feature] implemented and tested |
| M3: Beta | [date] | Feature-complete, internal users onboarded |
| M4: Launch | [date] | Public, monitored, documented |

---

## Open Questions

| # | Question | Owner | Due |
|---|---|---|---|
| 1 | [Question that needs answering before/during build] | [name] | [date] |
| 2 | | | |

---

## References

- [Link to product requirements document]
- [Link to design mockups]
- [Link to existing system documentation]
