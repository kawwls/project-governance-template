# Project Governance Template

Reusable governance starter for new software projects managed with this workflow:

- **Product Owner:** the user
- **Manager / Architect / Reviewer:** ChatGPT
- **Executor:** Antigravity
- **Source of truth:** GitHub `main`

This repository is intentionally product-agnostic and technology-agnostic. It contains no application framework, database, authentication provider, deployment stack, or product implementation.

## Included

```text
.agents/rules/executor-governance.md
.github/pull_request_template.md

docs/
├── MANAGER_WORKFLOW.md
├── REQUIREMENTS.md
├── ARCHITECTURE.md
├── LOCKED_DECISIONS.md
└── PROJECT_STATE.md

tasks/TASK_TEMPLATE.md
reports/REPORT_TEMPLATE.md
src/README.md
tests/README.md
```

## New Project Workflow

Create a new repository from this template, then:

```text
Idea
  ↓
Product Definition
  ↓
Requirements
  ↓
Architecture
  ↓
Locked Decisions
  ↓
TASK-0001
  ↓
Task Branch
  ↓
Antigravity Implementation
  ↓
Tests
  ↓
Pull Request
  ↓
ChatGPT Manager Review
  ↓
Merge
```

## First Steps in a New Project

1. Keep the governance files in place.
2. Tell ChatGPT the new repository and product idea.
3. Define the product before implementation.
4. Replace `NOT_DEFINED` placeholders in requirements and architecture only after approval.
5. Record product-specific locks.
6. Create `TASK-0001` from the task template.
7. Give the Executor only the approved task.
8. Review through a PR before merging.

## Important

Do not copy product-specific requirements, architecture, dependencies, or source code from a previous project unless they are explicitly approved for the new project.

Do not add a stack-specific `.gitignore` or initialize application code until the technology stack is approved.

See `docs/MANAGER_WORKFLOW.md` for the full operating model.
