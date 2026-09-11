# Manager Workflow

## Purpose
This repository uses a Product Owner / Manager / Executor workflow.

GitHub `main` is the approved source of truth for project state.

## Roles

### Product Owner
The user owns product intent, priorities, and final product decisions.

### Manager / Architect / Reviewer
ChatGPT acts as Manager, Architect, and Reviewer.

Responsibilities:
- turn product intent into an approved project charter and requirements;
- define architecture and technical direction;
- maintain locked decisions, quality gates, and project state;
- evaluate material change requests before implementation;
- create scoped implementation tasks;
- review implementation, tests, regressions, and scope compliance;
- approve or reject work for merge.

### Executor
Antigravity is the implementation executor.

Responsibilities:
- implement only approved tasks;
- follow `.agents/rules/executor-governance.md`;
- run required checks;
- commit/push the task branch;
- return `READY_FOR_REVIEW`, `BLOCKED`, or `TESTS_FAILED` as appropriate;
- never merge or self-approve.

## Source of Truth
Before planning or reviewing, read from `main`:
1. `GOVERNANCE_VERSION`
2. `docs/PROJECT_STATE.md`
3. `docs/PROJECT_CHARTER.md`
4. `docs/REQUIREMENTS.md`
5. `docs/ARCHITECTURE.md`
6. `docs/LOCKED_DECISIONS.md`
7. `docs/QUALITY_GATES.md`
8. the assigned task under `tasks/`
9. `.agents/rules/executor-governance.md` when executor constraints matter

A chat transcript is not the authoritative project state when it conflicts with the repository.

## Standard Workflow

```text
Idea
  ↓
Approved Project Charter
  ↓
Approved Requirements
  ↓
Approved Architecture
  ↓
Locked Decisions
  ↓
READY_FOR_IMPLEMENTATION gate
  ↓
TASK-XXXX
  ↓
Task Branch
  ↓
Executor Implementation
  ↓
Tests / Checks
  ↓
Pull Request
  ↓
Manager Review
  ├─ CHANGES_REQUIRED → Fix Loop → Review
  └─ APPROVED_FOR_MERGE → Merge
  ↓
Update Project State
```

Approval checkpoints are defined in `docs/QUALITY_GATES.md`.

## Manager-Owned Files
The Manager normally owns:
- `docs/PROJECT_CHARTER.md`
- `docs/REQUIREMENTS.md`
- `docs/ARCHITECTURE.md`
- `docs/LOCKED_DECISIONS.md`
- `docs/QUALITY_GATES.md`
- `docs/PROJECT_STATE.md`
- `docs/MANAGER_WORKFLOW.md`
- change requests under `changes/`
- task definitions under `tasks/`
- governance rules under `.agents/rules/`
- PR workflow templates

The Executor must not modify these unless the task explicitly authorizes it.

## Git and Review Rules
- `main` is approved truth.
- One implementation task should use one task branch and normally one PR.
- Executor work must not be performed directly on `main`.
- Antigravity must not merge or self-approve.
- Only the Product Owner or Manager may mark work `APPROVED_FOR_MERGE`.
- Failed review returns `CHANGES_REQUIRED` with specific findings.
- Fix rounds should address only the listed review findings unless new blocking evidence appears.

## Change Authority
Explicit Product Owner / Manager approval is required before changing:
- approved project scope;
- approved requirements;
- architecture;
- database/schema strategy;
- business rules;
- public API/data contracts;
- security boundaries;
- major UX flows;
- core framework/dependency direction;
- deployment architecture.

For material changes, create a change request from `changes/CHANGE_REQUEST_TEMPLATE.md` first. Review impact, alternatives, and affected control documents before implementation tasks are changed or created.

Small implementation choices that stay within approved requirements, architecture, locks, and task scope do not need a change request.

## Manager Review Format

Pass:

```text
MANAGER REVIEW

TASK: TASK-XXXX
RESULT: PASS

Scope              PASS
Requirements       PASS
Architecture       PASS
Locked Decisions   PASS
Implementation     PASS
Tests              PASS
Regression Risk    ACCEPTABLE

STATUS:
APPROVED_FOR_MERGE
```

Fail:

```text
MANAGER REVIEW

TASK: TASK-XXXX
RESULT: FAIL

Finding:
REV-001
...

STATUS:
CHANGES_REQUIRED
```

## New Project Bootstrap
When a repository is created from this template:
1. keep the governance skeleton;
2. identify the new product idea;
3. define and approve `docs/PROJECT_CHARTER.md`;
4. replace placeholder requirements with approved product requirements;
5. define and approve architecture before implementation;
6. record product/architecture locks;
7. update `docs/PROJECT_STATE.md`;
8. create `TASK-0001`;
9. only then assign implementation work.

Do not carry product-specific requirements or technology choices from another project unless explicitly approved for the new project.

## New Chat Bootstrap
Use `docs/BOOTSTRAP.md` rather than relying on prior chat context.

A new ChatGPT session should:
1. identify the target repository;
2. read the current control files from `main`;
3. inspect relevant open PR/task state;
4. continue from repository state instead of guessing stale context.

## Governance Versioning
`GOVERNANCE_VERSION` identifies the template governance version copied into a project. `CHANGELOG.md` records template evolution.

Existing projects do not automatically inherit future template changes. Upgrade governance only when the Product Owner / Manager intentionally chooses to do so and verifies that the change does not conflict with project-specific rules.
