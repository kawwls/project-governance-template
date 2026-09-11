# Project Governance Template

Reusable, technology-agnostic governance starter for software projects managed with this workflow:

- **Product Owner:** the user
- **Manager / Architect / Reviewer:** ChatGPT
- **Executor:** Antigravity
- **Source of truth:** GitHub `main`

Current governance version is stored in `GOVERNANCE_VERSION`. Changes to this template are recorded in `CHANGELOG.md`.

This repository intentionally contains no application framework, database, authentication provider, deployment stack, or product implementation.

## Included

```text
GOVERNANCE_VERSION
CHANGELOG.md

.agents/rules/executor-governance.md
.github/pull_request_template.md

docs/
├── BOOTSTRAP.md
├── MANAGER_WORKFLOW.md
├── PROJECT_CHARTER.md
├── REQUIREMENTS.md
├── ARCHITECTURE.md
├── LOCKED_DECISIONS.md
├── QUALITY_GATES.md
└── PROJECT_STATE.md

changes/CHANGE_REQUEST_TEMPLATE.md
tasks/TASK_TEMPLATE.md
reports/REPORT_TEMPLATE.md
src/README.md
tests/README.md
```

## New Project Workflow

```text
Idea
  ↓
Project Charter
  ↓
Requirements
  ↓
Architecture
  ↓
Locked Decisions
  ↓
Approved Task
  ↓
Task Branch
  ↓
Executor Implementation
  ↓
Tests
  ↓
Pull Request
  ↓
Manager Review
  ↓
Merge
```

Quality gates in `docs/QUALITY_GATES.md` define when each stage is actually approved.

## First Steps in a New Project
1. Create the project from this template.
2. Tell ChatGPT the repository name and product idea.
3. Approve `docs/PROJECT_CHARTER.md` before locking requirements.
4. Define and approve requirements and architecture.
5. Record project-specific locked decisions.
6. Update `docs/PROJECT_STATE.md`.
7. Create `TASK-0001` from the task template.
8. Give the Executor only the approved task.
9. Review through a PR before merging.

Use `docs/BOOTSTRAP.md` when starting a new ChatGPT session or handing a task to the Executor.

## Changes During a Project
A new idea is not automatically a new task. If it changes approved product scope, requirements, architecture, business rules, data contracts, security boundaries, major UX, or core dependencies, start from `changes/CHANGE_REQUEST_TEMPLATE.md` and approve the change before implementation.

Small implementation details that stay inside an approved task do not need a change request.

## Important
Do not copy product-specific requirements, architecture, dependencies, or source code from a previous project unless explicitly approved for the new project.

Do not add a stack-specific `.gitignore` or initialize application code until the technology stack is approved.

See `docs/MANAGER_WORKFLOW.md` for the operating model and `docs/QUALITY_GATES.md` for approval checkpoints.
