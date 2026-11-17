# Database Design — Conceptual Model (Draft)

**Document:** DB-001 | **Version:** 0.2 | **Status:** Conceptual only — no physical schema or migration approved  
**Companion:** [DD-001 Data Dictionary](DATA_DICTIONARY.md)

## 1. Purpose and principles

Define the logical information architecture for the PNG primary-school MVP. This document is not a PostgreSQL schema and does not authorise database provisioning or migrations.

- One school boundary per deployment is a candidate, not a final architecture decision.
- Use immutable internal identifiers; school-local student numbers are business identifiers, not primary keys.
- Preserve enrolment, grade, placement, attendance and assessment history.
- Keep grade enrolment separate from class-group membership to support mixed-grade classes.
- Keep curriculum framework, standards, criteria and judgements versioned and source-backed.
- Collect minimum necessary personal information.
- No hard deletion through normal school workflows.
- Physical schema, database vendor, RLS and migration strategy require separate review.

## 2. Logical domains

1. School and access: school, user account, school membership, role assignment, teacher assignment, audit event.
2. Academic structure: academic year, academic period, grade level, class group, class membership, subject.
3. Learner administration: student, enrolment, grade enrolment, placement, optional guardian contact.
4. Curriculum and assessment: curriculum framework, curriculum standard, assessment activity, criterion, evidence reference, achievement judgement, optional numeric score.
5. Attendance: attendance session and attendance record.
6. Reporting: report template, report issue, report section/value, export job.
7. Conditional offline: registered device/session, sync operation, sync conflict.

Detailed definitions, logical attributes, sensitivity and unresolved questions are in DD-001.

## 3. Core relationships

- One school owns its academic structure, users/memberships, learner records, configuration and reports.
- Academic year contains periods.
- Class group is a teaching organisation; learners join through dated membership.
- A learner's grade is stored separately in a dated grade-enrolment record.
- Learner placement and class membership preserve effective dates and history.
- Curriculum standards belong to a named framework/version and grade/subject.
- Assessment activities reference period, subject, applicable standards and criteria.
- Evidence and achievement judgements are learner-specific and trace to an activity/criterion.
- Attendance session belongs to a class group; attendance record links one learner to one session.
- Report issue references a period and exact template version; it does not mutate source records.
- All privileged and material changes are auditable.

## 4. Candidate integrity rules

- Unique school-local student number, subject to validated identifier policy.
- No duplicate active enrolment for the same school/time period without an authorised exception.
- No overlapping grade enrolment or class placement unless an explicit, auditable exception is allowed.
- Unique learner/session attendance record.
- Assessment and judgement must reference valid school, period, subject, learner and curriculum versions.
- Scores are optional and constrained only by an approved assessment scheme.
- Missing, pending, not assessed and zero are distinct states.
- Transfer/withdrawal does not cascade-delete history.
- Cross-school references are rejected at service and data boundaries.

## 5. Mixed-grade handling

A single class group may include learners from different grade levels. Model separately:
- class group and academic year;
- learner's grade enrolment for the period;
- dated class membership;
- subject/teacher assignment;
- curriculum framework, grade-specific standards and assessment criteria.

Reports and assessments must use each learner's applicable grade/standard, not infer it from the class label.

## 6. Security, privacy and audit

School isolation must be enforced beyond the UI. Exact database isolation/RLS design depends on the architecture decision. No service-role secret in client code. Audit actor, timestamp, action, affected record and reason where appropriate. Sensitive learner/staff data is not used in public repository examples or CI.

## 7. Offline data model (conditional)

If offline capture is approved, each mutation needs a unique operation ID, authorised user/device/session context, client and server timestamps, idempotent retry handling and a visible resolution state. Conflicts must not silently overwrite academic data. The offline model is excluded from production until the offline release gate passes.

## 8. Decisions intentionally deferred

Physical table/column names and types; indexes; SQL constraints; RLS; tenant topology; auth provider; retention schedules; exact attendance code list; curriculum import format; evidence file storage; score schema; national identifiers; API and migrations.

## 9. Approval gate

The conceptual model must be reconciled with approved requirements, school workflows, privacy/security threat model and deployment/isolation architecture. Only then may a physical schema proposal be prepared for explicit review. No database migration is authorised by this document.
