# Quality Gates

These gates keep repository verification, planning, implementation, and release decisions separate.

## GATE-00 — REPO_VERIFIED
Required evidence:
- exact target `OWNER/REPO` exists on GitHub;
- GitHub `main` is readable;
- `GOVERNANCE_VERSION` and required control documents are readable from that repo.

If any check fails, status is `REPO_NOT_VERIFIED` and the workflow stops immediately.

Before GATE-00 passes, the Manager must not:
- inspect local folders for a substitute project/template;
- copy, move, adapt, create, or edit project files;
- create branches or task files;
- initialize frameworks/dependencies;
- generate implementation assets;
- run implementation/build/dev/test/preview commands;
- open a local preview;
- fabricate/infer repository state;
- rewrite governance version to match a requested version.

Allowed response on failure: state the blocking reason and exact user action needed to continue. Planning discussion in chat is allowed, but no repository-backed or local implementation activity is allowed.

A local checkout can be used only after GATE-00 passes and it is verified to correspond to the same GitHub repo.

## GATE-01 — PRODUCT_DEFINED
Required evidence:
- `docs/PROJECT_CHARTER.md` approved;
- problem, target user, scope, and success criteria are clear;
- explicit Product Owner approval recorded in chat or repository state.

Blocks:
- requirements approval if product intent is unclear.

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
- implementation task approval if architecture/contracts remain undecided.

## GATE-04 — READY_FOR_IMPLEMENTATION
Required evidence:
- GATE-00 through GATE-03 passed;
- an approved task file exists;
- branch, scope, acceptance criteria, constraints, and required tests are defined;
- no unresolved blocker affects the task;
- explicit Product Owner approval to hand the task to the Executor.

Only after this gate may implementation begin.

## GATE-05 — READY_FOR_MERGE
Required evidence:
- implementation matches approved scope;
- required tests/checks actually ran with acceptable results;
- review findings are resolved;
- Manager status is `APPROVED_FOR_MERGE`.

## GATE-06 — READY_FOR_RELEASE
Use only when the project has a release concept. Define project-specific release criteria before declaring release readiness.

## Manager Hard Stop
Before GATE-04 passes, the Manager must not:
- write product implementation code;
- initialize/change the application framework for implementation;
- create an implementation branch;
- generate product assets intended for implementation;
- run implementation/build commands as the Executor;
- silently act as the Executor.

Before GATE-04, after GATE-00 has passed, the Manager may read the verified repository, analyze options, edit Manager-owned planning/control documents, and create/revise the task definition needed for approval.

## Rule
Passing one gate does not imply later gates pass. The Product Owner must explicitly approve GATE-01 through GATE-04 before crossing them. Executors can report implementation/test status but cannot approve governance gates.
