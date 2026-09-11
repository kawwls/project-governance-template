# Quality Gates

These gates keep planning, implementation, and release decisions separate.

## GATE-01 — PRODUCT_DEFINED
Required evidence:
- `docs/PROJECT_CHARTER.md` approved
- problem, target user, scope, and success criteria are clear

Blocks:
- requirements approval if product intent is still unclear

## GATE-02 — REQUIREMENTS_APPROVED
Required evidence:
- `docs/REQUIREMENTS.md` approved
- major business rules and acceptance expectations are explicit

Blocks:
- architecture approval if requirements are unstable

## GATE-03 — ARCHITECTURE_APPROVED
Required evidence:
- `docs/ARCHITECTURE.md` approved
- important technical choices recorded in `docs/LOCKED_DECISIONS.md`

Blocks:
- implementation tasks that depend on undecided architecture

## GATE-04 — READY_FOR_IMPLEMENTATION
Required evidence:
- approved task exists
- branch, scope, acceptance criteria, constraints, and required tests are defined
- no unresolved blocker affecting the task

## GATE-05 — READY_FOR_MERGE
Required evidence:
- implementation matches approved scope
- required tests/checks actually ran with acceptable results
- review findings are resolved
- Manager status is `APPROVED_FOR_MERGE`

## GATE-06 — READY_FOR_RELEASE
Use only when the project has a release concept.
Required evidence should be defined by project-specific release criteria before declaring a release ready.

## Rule
Passing one gate does not imply later gates are passed. Executors may report implementation/test status, but only the Product Owner or Manager may approve governance gates.
