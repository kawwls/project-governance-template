# TASK-XXXX

## Goal
Describe exactly what must be completed.

## Branch
`branch-name`

## Context
List the approved project context and why this task exists.

## In Scope
- Work explicitly allowed in this task.

## Out of Scope
- Work that must not be done.

## Requirements
1. Requirement 1
2. Requirement 2

## Constraints
- Do not change approved architecture unless explicitly authorized.
- Do not expand scope.
- Do not make unrelated changes.
- Do not modify Manager-owned files unless explicitly authorized.

## Acceptance Criteria
- AC01:
- AC02:

## Required Tests / Checks
- List the exact tests, checks, builds, or manual verification required.

## Approval Gate
Do not hand this task to the Executor until `READY_FOR_IMPLEMENTATION` is explicitly approved by the Product Owner.

## Manager Handoff
After approval, the Manager should return a compact Antigravity prompt that references this task instead of repeating it:

```text
TASK-XXXX — EXECUTE
Repo: OWNER/REPO
Branch: branch-name

Read `.agents/rules/executor-governance.md`, the current control docs, and this task file in full.
Implement exactly this task. No scope/architecture/contract expansion.
Run every required check. Commit + push the same branch. Do not merge.
Return the required governance completion report. Contract/scope blocker -> BLOCKED.
```

## Completion
Commit and push the task branch.

Return the completion report required by `.agents/rules/executor-governance.md`.

Use only an allowed executor status such as `READY_FOR_REVIEW`, `BLOCKED`, or `TESTS_FAILED` as appropriate.

Do not merge into `main` and do not self-approve.
