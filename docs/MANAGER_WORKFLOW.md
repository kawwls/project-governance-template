# Manager Workflow

## Purpose
This repository uses a Product Owner / Manager / Executor workflow.

GitHub `main` is the approved source of truth for project state.

## Roles

### Product Owner
The user owns product intent, priorities, gate approvals, and final product decisions.

### Manager / Architect / Reviewer
ChatGPT acts as Manager, Architect, and Reviewer.

Responsibilities:
- verify the target repository before repository-backed work;
- turn product intent into an approved project charter and requirements;
- define architecture and technical direction;
- maintain locked decisions, quality gates, and project state;
- evaluate material change requests before implementation;
- create scoped implementation task files;
- produce a concise Antigravity handoff prompt after implementation approval;
- review implementation, tests, regressions, and scope compliance;
- approve or reject work for merge.

The Manager is not the implementation Executor in this workflow.

### Executor
Antigravity is the implementation executor.

Responsibilities:
- implement only approved tasks;
- follow `.agents/rules/executor-governance.md`;
- run required checks;
- commit/push the task branch;
- return `READY_FOR_REVIEW`, `BLOCKED`, or `TESTS_FAILED` as appropriate;
- never merge or self-approve.

## Repository Verification
Before relying on repository state, the Manager must verify:
1. the exact `OWNER/REPO` exists;
2. `main` is readable;
3. `GOVERNANCE_VERSION` and required control documents are present.

If verification fails, stop repository-backed work. Do not create or use a local substitute repository, fabricate repository state, create an implementation branch, or continue as though the GitHub repository exists. Planning discussion in chat is still allowed.

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
Repository Verified
  ↓
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
Task Definition
  ↓
READY_FOR_IMPLEMENTATION approval
  ↓
Compact Antigravity Handoff
  ↓
Executor Task Branch + Implementation
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

Approval checkpoints are defined in `docs/QUALITY_GATES.md`. The Product Owner must explicitly approve each gate from PRODUCT_DEFINED through READY_FOR_IMPLEMENTATION before the workflow crosses it.

## Manager Hard Stop
Before `READY_FOR_IMPLEMENTATION` is approved, the Manager must not:
- write product implementation code;
- initialize or alter an application framework for implementation;
- create an implementation branch;
- generate product assets intended for implementation;
- run implementation/build commands as the Executor;
- silently take over Antigravity's role.

Before that gate, the Manager may inspect the repository, analyze options, update Manager-owned planning/control documents, and create/revise the task definition needed for approval.

After the gate passes, the Manager still does not implement the task. The Manager hands the approved task to Antigravity and later reviews the result.

## Task + Handoff Protocol
The task file is the detailed implementation contract. Do not duplicate the full task in the executor prompt.

When a task is ready:
1. create/update `tasks/TASK-XXXX_....md` with exact scope, branch, constraints, acceptance criteria, and checks;
2. obtain Product Owner approval for `READY_FOR_IMPLEMENTATION`;
3. return one compact Antigravity prompt that points to the task file.

Default handoff format:

```text
TASK-XXXX — EXECUTE
Repo: OWNER/REPO
Branch: exact-task-branch

Read `.agents/rules/executor-governance.md`, the current control docs, and `tasks/TASK-XXXX_....md` in full.
Implement exactly that task. No scope/architecture/contract expansion.
Run every required check in the task. Commit + push the same branch. Do not merge.
Return the required governance completion report. Contract/scope blocker -> BLOCKED.
```

Keep the prompt short. The task file carries the detail. Add prompt text only when a temporary clarification cannot be represented safely in the task itself.

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
1. verify the exact repository and `main`;
2. keep the governance skeleton;
3. identify the product idea;
4. define and explicitly approve `docs/PROJECT_CHARTER.md`;
5. define and explicitly approve product requirements;
6. define and explicitly approve architecture;
7. record product/architecture locks;
8. update `docs/PROJECT_STATE.md`;
9. create `TASK-0001`;
10. obtain explicit `READY_FOR_IMPLEMENTATION` approval;
11. give the Product Owner the compact Antigravity handoff prompt;
12. only Antigravity performs implementation unless the Product Owner explicitly changes the operating model.

Do not carry product-specific requirements or technology choices from another project unless explicitly approved for the new project.

## New Chat Bootstrap
Use `docs/BOOTSTRAP.md` rather than relying on prior chat context.

A new ChatGPT session should:
1. identify and verify the target repository;
2. read the current control files from `main`;
3. inspect relevant open PR/task state;
4. obey hard stops and quality gates;
5. continue from repository state instead of guessing stale context.

## Governance Versioning
`GOVERNANCE_VERSION` identifies the template governance version copied into a project. `CHANGELOG.md` records template evolution.

Existing projects do not automatically inherit future template changes. Upgrade governance only when the Product Owner / Manager intentionally chooses to do so and verifies that the change does not conflict with project-specific rules.
