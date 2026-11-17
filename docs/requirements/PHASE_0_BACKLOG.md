# Phase 0 — Foundation Backlog

**Status:** Proposed issue register; create/link GitHub Issues before implementation.

| ID | Work item | Deliverable | Dependency |
|---|---|---|---|
| P0-01 | Confirm project charter and MVP boundaries | Approved charter | None |
| P0-02 | Research PNG primary education requirements | Source-backed curriculum/reporting validation register | P0-01 |
| P0-03 | Validate school workflows with reference school | Workflow findings and open questions | P0-01 |
| P0-04 | Complete functional/non-functional requirements | Approved PRD | P0-02, P0-03 |
| P0-05 | Define data dictionary and entity relationships | Reviewed database specification | P0-04 |
| P0-06 | Decide school deployment/database isolation | Architecture decision record | P0-05 |
| P0-07 | Define roles, permissions and threat model | Security design and test cases | P0-04, P0-06 |
| P0-08 | Specify offline and sync behaviour | Offline design and conflict policy | P0-05, P0-06 |
| P0-09 | Finalise report-card and report catalogue | Approved report specification | P0-02, P0-03 |
| P0-10 | Select and validate technology stack | Architecture baseline and cost assessment | P0-06, P0-07, P0-08 |
| P0-11 | Define backup, restore and deployment process | Operational readiness plan | P0-06, P0-10 |
| P0-12 | Finalise MVP acceptance and test strategy | Traceable test plan | P0-04 to P0-11 |
| P0-13 | Establish repository CI and contribution controls | Passing baseline workflow | P0-10 |
| P0-14 | Approve Release 1 implementation backlog | Prioritised GitHub milestone/issues | P0-12, P0-13 |

## Batch guidance

- Batch 1: P0-01 to P0-03 (scope and discovery).
- Batch 2: P0-04 to P0-06 (requirements and data/architecture foundations).
- Batch 3: P0-07 to P0-09 (security, offline and reporting).
- Batch 4: P0-10 to P0-13 (technology and delivery readiness).
- Batch 5: P0-14 (implementation backlog and release gate).

Do not create production schema or process real learner data during Phase 0.
