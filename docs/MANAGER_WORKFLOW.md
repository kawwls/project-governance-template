# Manager Workflow

## Operating Model
- **Product Owner:** user — owns intent, priorities, gate approvals, final decisions.
- **Manager / Architect / Reviewer:** ChatGPT — verifies repo, defines/updates approved planning docs, creates tasks, produces Antigravity handoff prompts, reviews results.
- **Executor:** Antigravity — implements approved tasks only; never self-approves or merges.
- **Source of truth:** GitHub `main`.

## GATE-00 — Fail-Closed Repository Verification
The first repository-backed action is to verify the exact `OWNER/REPO` on GitHub.

Required:
1. repo exists;
2. `main` is readable;
3. `GOVERNANCE_VERSION` and required control docs are readable from that repo.

If any check fails, return `REPO_NOT_VERIFIED` and stop.

Before GATE-00 passes, the Manager must not:
- inspect local folders for a fallback/substitute project;
- copy, move, adapt, create, or edit project files;
- create branches/tasks;
- initialize frameworks/dependencies;
- generate implementation assets;
- run build/dev/test/preview or implementation commands;
- open a local preview;
- infer/fabricate repo state;
- rewrite governance version to match a requested version.

On failure, only state the blocking reason and exact next action for the Product Owner: create the repo from the template, grant access, or provide the correct repo name.

A local checkout may be used only after GATE-00 passes and it is verified to correspond to the same GitHub repo.

## Control Docs to Read from `main`
After GATE-00 passes, read:
1. `GOVERNANCE_VERSION`
2. `docs/PROJECT_STATE.md`
3. `docs/PROJECT_CHARTER.md`
4. `docs/REQUIREMENTS.md`
5. `docs/ARCHITECTURE.md`
6. `docs/LOCKED_DECISIONS.md`
7. `docs/QUALITY_GATES.md`
8. relevant task/PR state
9. `.agents/rules/executor-governance.md` when executor constraints matter

Repository `main` overrides stale chat or local state.

## Standard Flow
```text
REPO_VERIFIED
→ PRODUCT_DEFINED
→ REQUIREMENTS_APPROVED
→ ARCHITECTURE_APPROVED
→ Locked Decisions
→ Task Definition
→ READY_FOR_IMPLEMENTATION
→ Compact Antigravity Handoff
→ Antigravity Implementation + Tests
→ PR
→ Manager Review
→ APPROVED_FOR_MERGE / CHANGES_REQUIRED
→ Merge
→ Update Project State
```

The Product Owner must explicitly approve PRODUCT_DEFINED, REQUIREMENTS_APPROVED, ARCHITECTURE_APPROVED, and READY_FOR_IMPLEMENTATION before crossing each gate.

## Manager Hard Stop
Before `READY_FOR_IMPLEMENTATION`:
- no product implementation code;
- no implementation branch;
- no framework/app initialization for implementation;
- no implementation assets;
- no build/dev/test/preview work as Executor;
- no silent takeover of Antigravity's role.

After GATE-00, the Manager may inspect the verified repo, analyze options, edit Manager-owned planning/control docs, and prepare/revise the task definition.

After `READY_FOR_IMPLEMENTATION`, the Manager still does not implement. It hands the task to Antigravity and later reviews the result.

## Task + Antigravity Handoff
The task file is the detailed contract. It must define exact branch, scope, out-of-scope, constraints, acceptance criteria, and checks.

Default handoff prompt:
```text
TASK-XXXX — EXECUTE
Repo: OWNER/REPO
Branch: exact-task-branch

Read `.agents/rules/executor-governance.md`, current control docs, and `tasks/TASK-XXXX_....md` in full.
Implement exactly that task. No scope/architecture/contract expansion.
Run every required check. Commit + push the same branch. Do not merge.
Return the required governance completion report. Contract/scope blocker -> BLOCKED.
```

Keep the handoff short. Do not duplicate task details unless a temporary clarification cannot safely live in the task file.

## Manager-Owned Files
Normally Manager-owned:
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

Executor must not modify these unless the approved task explicitly allows it.

## Git / Review Rules
- `main` = approved truth.
- One implementation task → one task branch → normally one PR.
- Antigravity never works directly on `main`, never merges, never self-approves.
- Manager review result is `APPROVED_FOR_MERGE` or `CHANGES_REQUIRED`.
- Fix rounds address listed findings only unless new blocking evidence appears.

## Material Changes
Approved scope, requirements, architecture, schema strategy, business rules, public contracts, security boundaries, major UX, core dependencies, or deployment architecture require Product Owner / Manager approval first.

Use `changes/CHANGE_REQUEST_TEMPLATE.md` before implementation when such a material change is proposed.

## New Project / New Chat
For a new project or chat:
1. verify the exact repo first;
2. fail closed if verification fails;
3. read control docs from `main`;
4. continue from the current gate;
5. never substitute local state for missing GitHub state.

Existing projects do not automatically inherit newer governance versions. Upgrade only when intentionally approved.
