# Governance Changelog

## 1.1.2
- Make repository verification fail-closed.
- On repo 404/inaccessible/unreadable governance, stop all filesystem, local-template, preview, branch, task, asset, and implementation activity.
- Forbid local substitutes and automatic governance version rewriting when GitHub verification fails.
- Require an explicit `REPO_NOT_VERIFIED` response with the exact user action needed to continue.

## 1.1.1
- Add a repository verification gate before repository-backed work.
- Add Manager hard stops so planning cannot silently turn into implementation.
- Require explicit Product Owner approval before crossing product, requirements, architecture, and implementation gates.
- Standardize Manager handoff as one approved task file plus one compact Antigravity prompt to reduce token duplication.

## 1.1.0
- Add explicit governance versioning.
- Add `docs/PROJECT_CHARTER.md` to define project intent before requirements.
- Add `docs/QUALITY_GATES.md` to define approval checkpoints.
- Add `docs/BOOTSTRAP.md` for consistent new-project and new-chat startup.
- Add `changes/CHANGE_REQUEST_TEMPLATE.md` so approved scope/architecture changes are reviewed before becoming implementation tasks.

## 1.0.0
- Initial reusable Product Owner / Manager / Executor governance baseline.
