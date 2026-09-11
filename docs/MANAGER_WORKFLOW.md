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
- turn product intent into approved requirements;
- define architecture and technical direction;
- maintain locked decisions and project state;
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
1. `docs/PROJECT_STATE.md`
2. `docs/REQUIREMENTS.md`
3. `docs/ARCHITECTURE.md`
4. `docs/LOCKED_DECISIONS.md`
5. the assigned task under `tasks/`
6. `.agents/rules/executor-governance.md` when executor constraints matter

A chat transcript is not the authoritative project state when it conflicts with the repository.

## Standard Workflow

```text
Idea
  ↓
Product Definition
  ↓
Approved Requirements
  ↓
Approved Architecture
  ↓
Locked Decisions
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

## Manager-Owned Files
The Manager normally owns:
- `docs/REQUIREMENTS.md`
- `docs/ARCHITECTURE.md`
- `docs/LOCKED_DECISIONS.md`
- `docs/PROJECT_STATE.md`
- `docs/MANAGER_WORKFLOW.md`
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
Explicit Manager approval is required before changing:
- approved requirements;
- architecture;
- database/schema strategy;
- business rules;
- public API/data contracts;
- security boundaries;
- major UX flows;
- core framework/dependency direction;
- deployment architecture.

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
3. replace placeholder requirements with approved product requirements;
4. define and approve architecture before implementation;
5. record product/architecture locks;
6. update `docs/PROJECT_STATE.md`;
7. create `TASK-0001`;
8. only then assign implementation work.

Do not carry product-specific requirements or technology choices from another project unless explicitly approved for the new project.

## New Chat Bootstrap
A new ChatGPT session should not rely on prior chat context as authoritative.

Before continuing project work:
1. identify the target repository;
2. read this file and the current control files from `main`;
3. inspect relevant open PR/task state;
4. continue from repository state instead of guessing stale context.
