# Bootstrap Guide

Use this file to start consistently without relying on old chat context.

## New Project from This Template
1. Create a new repository from this template.
2. Tell the Manager the exact `OWNER/REPO` and project idea.
3. Manager verifies the repository and reads `main` before repository-backed work.
4. Define and approve `docs/PROJECT_CHARTER.md`.
5. Define and approve requirements.
6. Define and approve architecture and locked decisions.
7. Manager creates the approved task definition.
8. Product Owner approves `READY_FOR_IMPLEMENTATION`.
9. Manager returns one compact Antigravity handoff prompt that references the task file.
10. Antigravity implements; Manager reviews; Product Owner/Manager controls merge.

## New Chat — Manager Bootstrap Prompt
```text
Use repository OWNER/REPO as the source of truth.
I am the Product Owner.
You are the Manager + Architect + Reviewer.
Antigravity is the Executor.

First verify the exact repository exists and main is readable. If not, STOP repository-backed work; do not invent a local substitute.

Read from main:
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

Read `.agents/rules/executor-governance.md`, the current control docs, and `tasks/TASK-XXXX_....md` in full.
Implement exactly that task. No scope/architecture/contract expansion.
Run every required check in the task. Commit + push the same branch. Do not merge.
Return the required governance completion report. Contract/scope blocker -> BLOCKED.
```

The task file is the detailed source of truth. Keep the handoff prompt short; do not duplicate requirements, acceptance criteria, or test lists unless a temporary clarification is essential.

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
Repository `main` overrides stale chat context. If the repository is unavailable or control documents conflict, stop and resolve that first. Manager planning and Executor implementation are separate phases and separate roles.
