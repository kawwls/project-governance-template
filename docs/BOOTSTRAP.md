# Bootstrap Guide

Use this file to start consistently without relying on old chat context.

## New Project from This Template
1. Create a new repository from this template.
2. Tell the Manager the exact `OWNER/REPO` and project idea.
3. Manager verifies that exact GitHub repository and reads `main`.
4. If verification fails, stop completely and ask for the missing repo/access/correct name.
5. Define and approve `docs/PROJECT_CHARTER.md`.
6. Define and approve requirements.
7. Define and approve architecture and locked decisions.
8. Manager creates the approved task definition.
9. Product Owner approves `READY_FOR_IMPLEMENTATION`.
10. Manager returns one compact Antigravity handoff prompt that references the task file.
11. Antigravity implements; Manager reviews; Product Owner/Manager controls merge.

## Fail-Closed Repository Check
Repository verification is the first repository-backed action.

Verification requires:
- exact `OWNER/REPO` exists on GitHub;
- `main` is readable;
- `GOVERNANCE_VERSION` and required control docs are readable from that repo.

If any check fails, status is `REPO_NOT_VERIFIED` and the workflow stops.

Before verification passes, do **not**:
- inspect local folders for a substitute project/template;
- copy/move/adapt local template files;
- create or edit local/remote project files;
- create branches or tasks;
- initialize frameworks or dependencies;
- generate implementation assets;
- run build/dev/test/preview commands;
- open a local preview;
- infer or fabricate repo state;
- rewrite governance version to match the requested version.

Only return the blocking reason and exact user action needed, for example: create the repo from the template, grant repository access, or provide the correct `OWNER/REPO`.

A local checkout may be used only after GATE-00 passes and it is proven to correspond to the same verified GitHub repository.

## New Chat — Manager Bootstrap Prompt
```text
Use repository OWNER/REPO as the source of truth.
I am the Product Owner.
You are the Manager + Architect + Reviewer.
Antigravity is the Executor.

FIRST: verify that exact GitHub repo exists and `main` + governance files are readable.
If verification fails: return REPO_NOT_VERIFIED and STOP. No local fallback, filesystem search, file changes, branches, tasks, assets, commands, preview, implementation, or governance-version rewriting.

After verification passes, read from main:
- GOVERNANCE_VERSION
- docs/MANAGER_WORKFLOW.md
- docs/PROJECT_STATE.md
- docs/PROJECT_CHARTER.md
- docs/REQUIREMENTS.md
- docs/ARCHITECTURE.md
- docs/LOCKED_DECISIONS.md
- docs/QUALITY_GATES.md
- relevant task/PR state

Follow the quality gates. Do not implement product code yourself.
Before READY_FOR_IMPLEMENTATION, only plan/update Manager-owned docs and prepare the task.
At each gate, wait for my explicit approval before crossing it.
When READY_FOR_IMPLEMENTATION is approved, create/update the task file and give me one concise Antigravity prompt that references that task instead of repeating its full contents.
Continue from repository state; do not guess from stale chat context.
```

## Compact Antigravity Handoff
Use this format after GATE-04 is approved:

```text
TASK-XXXX — EXECUTE
Repo: OWNER/REPO
Branch: exact-task-branch

Read `.agents/rules/executor-governance.md`, current control docs, and `tasks/TASK-XXXX_....md` in full.
Implement exactly that task. No scope/architecture/contract expansion.
Run every required check. Commit + push the same branch. Do not merge.
Return the required governance completion report. Contract/scope blocker -> BLOCKED.
```

The task file is the detailed source of truth. Keep the handoff prompt short; do not duplicate requirements, acceptance criteria, or test lists unless temporary clarification is essential.

## Executor Bootstrap Prompt
```text
Before implementation, read:
- .agents/rules/executor-governance.md
- docs/PROJECT_STATE.md
- docs/REQUIREMENTS.md
- docs/ARCHITECTURE.md
- docs/LOCKED_DECISIONS.md
- the assigned task in full

Verify the exact task branch. Execute only approved scope, run required checks, commit/push, do not merge, and return the governance completion report.
```

## Rule
GitHub `main` overrides stale chat and local state. If the repository is unavailable or control documents conflict, stop and resolve that first. Manager planning and Executor implementation are separate phases and roles.
