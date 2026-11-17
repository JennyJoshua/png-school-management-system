# Phase 0 — Foundation Backlog

**Status:** Discovery and design only. Issues #1–#14 are open; no production code, physical database schema, migrations or real learner-data processing is authorised by this backlog.

| ID | Work item | GitHub Issue | Deliverable | Dependency |
|---|---|---|---|---|
| P0-01 | Confirm charter and Release 1 boundaries | [#1](https://github.com/JennyJoshua/png-school-management-system/issues/1) | Approved charter and authority record | None |
| P0-02 | Validate PNG curriculum, assessment and reporting | [#2](https://github.com/JennyJoshua/png-school-management-system/issues/2) | Evidence register with current-status limitations | #1 |
| P0-03 | Validate reference-school workflows | [#3](https://github.com/JennyJoshua/png-school-management-system/issues/3) | Workflow maps and authority sign-off | #1, #2 |
| P0-04 | Reconcile functional/non-functional requirements | [#4](https://github.com/JennyJoshua/png-school-management-system/issues/4) | Traceable approved PRD | #1–#3 |
| P0-05 | Data dictionary and conceptual model | [#5](https://github.com/JennyJoshua/png-school-management-system/issues/5) | Reviewed technology-neutral model | #4 |
| P0-06 | School deployment/database isolation | [#6](https://github.com/JennyJoshua/png-school-management-system/issues/6) | ADR and 1/10/50-school cost model | #5 |
| P0-07 | Privacy, security and threat model | [#7](https://github.com/JennyJoshua/png-school-management-system/issues/7) | Threat register, privacy inventory, permission matrix | #4, #6 |
| P0-08 | Offline/sync release gate | [#8](https://github.com/JennyJoshua/png-school-management-system/issues/8) | Offline design and online-only fallback | #5–#7 |
| P0-09 | Report catalogue and report-card validation | [#9](https://github.com/JennyJoshua/png-school-management-system/issues/9) | Approved report field register | #2–#4 |
| P0-10 | Technology stack and operating costs | [#10](https://github.com/JennyJoshua/png-school-management-system/issues/10) | Options matrix and cost assessment | #6–#8 |
| P0-11 | Backup, restore and operational readiness | [#11](https://github.com/JennyJoshua/png-school-management-system/issues/11) | Runbook and restore evidence | #6, #10 |
| P0-12 | MVP acceptance and test strategy | [#12](https://github.com/JennyJoshua/png-school-management-system/issues/12) | Traceable test plan and release gates | #4–#11 |
| P0-13 | Repository CI and contribution controls | [#13](https://github.com/JennyJoshua/png-school-management-system/issues/13) | Tested quality workflow | #10 |
| P0-14 | Approve Release 1 implementation backlog | [#14](https://github.com/JennyJoshua/png-school-management-system/issues/14) | Prioritised, approved implementation backlog | #4–#13 |

## Delivery sequence

- Batch 1 — scope and discovery: P0-01 to P0-03.
- Batch 2 — requirements and data model: P0-04 to P0-05.
- Batch 3 — architecture, security and offline decision: P0-06 to P0-08.
- Batch 4 — reporting and operational readiness: P0-09 to P0-11.
- Batch 5 — test/CI and implementation backlog gate: P0-12 to P0-14.

Dependencies are recorded in each issue. P0-03 depends on initial P0-02 research so school observations are interpreted against published evidence; it still requires a second-school or competent-authority cross-check before making national/provincial claims.

## Repository hygiene and governance

Use no invented assignees or arbitrary due dates. Add labels/milestones only when their definitions and ownership are agreed. Do not close an issue until its acceptance criteria and evidence are satisfied. The charter and technical documents remain Draft until the approval mechanism in PC-001 is completed.

## Stop gates

No production implementation, physical database schema, hosted database migration, paid infrastructure, production deployment or real learner-data processing during Phase 0. Use synthetic/de-identified information. Never commit staff names, signatures, school letterheads, identifiable scans or unredacted screenshots.