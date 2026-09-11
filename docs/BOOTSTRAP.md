# Bootstrap Guide

Use this file to start consistently without relying on old chat context.

## New Project from This Template
1. Create a new repository from the template.
2. Keep governance files unchanged initially.
3. Tell the Manager the repository name and project idea.
4. Define and approve `docs/PROJECT_CHARTER.md`.
5. Define and approve requirements.
6. Define and approve architecture.
7. Record locked decisions.
8. Update project state.
9. Create the first approved implementation task.
10. Only then assign work to the Executor.

## New Chat — Manager Bootstrap Prompt
```text
Use repository OWNER/REPO as the source of truth.
I am the Product Owner.
You are the Manager + Architect + Reviewer.
Antigravity is the Executor.

Before continuing, read from main:
- GOVERNANCE_VERSION
- docs/MANAGER_WORKFLOW.md
- docs/PROJECT_STATE.md
- docs/PROJECT_CHARTER.md
- docs/REQUIREMENTS.md
- docs/ARCHITECTURE.md
- docs/LOCKED_DECISIONS.md
- docs/QUALITY_GATES.md
- the relevant task/PR state

Continue from repository state. Do not guess from stale chat context.
```

## Executor Bootstrap Prompt
```text
Before implementation, read:
- .agents/rules/executor-governance.md
- docs/PROJECT_STATE.md
- docs/REQUIREMENTS.md
- docs/ARCHITECTURE.md
- docs/LOCKED_DECISIONS.md
- the assigned task in full

Verify the required task branch, execute only approved scope, run required checks, commit/push, do not merge, and return the governance completion report.
```

## Rule
Repository `main` overrides stale chat context. If repository documents conflict with each other, stop and resolve the conflict before implementation.
