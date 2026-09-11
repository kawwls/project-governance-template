# Quality Gates

These gates keep repository verification, planning, implementation, and release decisions separate.

## GATE-00 — REPO_VERIFIED
Required evidence:
- the exact target repository exists;
- GitHub `main` is readable;
- `GOVERNANCE_VERSION` and the control documents are present.

If the repository is missing, inaccessible, or not created from the expected template, STOP repository-backed work. The Manager may discuss or draft ideas in chat, but must not create a local substitute repository, implementation branch, product code, or fake repository state.

## GATE-01 — PRODUCT_DEFINED
Required evidence:
- `docs/PROJECT_CHARTER.md` approved;
- problem, target user, scope, and success criteria are clear;
- explicit Product Owner approval recorded in chat or repository state.

Blocks:
- requirements approval if product intent is still unclear.

## GATE-02 — REQUIREMENTS_APPROVED
Required evidence:
- `docs/REQUIREMENTS.md` approved;
- major business rules and acceptance expectations are explicit;
- explicit Product Owner approval recorded.

Blocks:
- architecture approval if requirements are unstable.

## GATE-03 — ARCHITECTURE_APPROVED
Required evidence:
- `docs/ARCHITECTURE.md` approved;
- important technical choices recorded in `docs/LOCKED_DECISIONS.md`;
- explicit Product Owner approval recorded.

Blocks:
- implementation task approval if architecture or important contracts remain undecided.

## GATE-04 — READY_FOR_IMPLEMENTATION
Required evidence:
- GATE-00 through GATE-03 passed;
- an approved task file exists;
- branch, scope, acceptance criteria, constraints, and required tests are defined;
- no unresolved blocker affecting the task;
- explicit Product Owner approval to hand the task to the Executor.

Only after this gate may implementation begin.

## GATE-05 — READY_FOR_MERGE
Required evidence:
- implementation matches approved scope;
- required tests/checks actually ran with acceptable results;
- review findings are resolved;
- Manager status is `APPROVED_FOR_MERGE`.

## GATE-06 — READY_FOR_RELEASE
Use only when the project has a release concept.
Required evidence should be defined by project-specific release criteria before declaring a release ready.

## Hard Stop
Before GATE-04 passes, the Manager must not:
- write product implementation code;
- initialize or change the application framework for implementation;
- create an implementation branch;
- generate product assets intended for the implementation;
- run implementation/build commands as the Executor;
- silently act as the Executor.

Before GATE-04, the Manager may read the repository, analyze, edit Manager-owned planning/control documents, and create or revise the task definition needed for approval.

## Rule
Passing one gate does not imply later gates are passed. The Product Owner must explicitly approve GATE-01 through GATE-04 before the workflow crosses them. Executors may report implementation/test status, but they cannot approve governance gates.
