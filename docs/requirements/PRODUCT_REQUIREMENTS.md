# Product Requirements — Release 1 MVP

**Document:** PRD-001 | **Version:** 0.3 | **Status:** Draft for review

## 1. Product outcome

A school maintains trusted enrolment, attendance and assessment records and produces accurate reports aligned with its validated curriculum and approved local reporting practice.

## 2. Personas

- Head teacher / school administrator.
- Class teacher.
- Subject teacher.
- Read-only report viewer with explicit permissions.

A user may hold multiple roles in a small school, but access remains least-privilege and school-scoped. No shared accounts.

## 3. Functional requirements

### FR-01 School setup
Maintain school profile, verified identifiers where available, location, contact and configuration. Do not invent official identifiers.

### FR-02 Academic structure and mixed-grade classes
Configure academic years/periods, grade levels, class groups, streams, subjects and teacher assignments. Primary MVP defaults to Grades 3–8. Prep–Grade 2 remains a separate elementary stage and excluded unless scope changes. Support a class group containing learners from more than one grade without collapsing their individual enrolled grade, curriculum grade or assessment standards. Record the class group and grade-specific subject/standard assignment separately. Grade 2→3 is a stage transition, not an ordinary primary promotion.

### FR-03 Student register and enrolment
Maintain minimum necessary learner identity and enrolment information. Support active, transferred, withdrawn and completed statuses. Preserve history and avoid hard deletion through normal workflows. Confirm mandatory fields and retention rules before release.

### FR-04 Class placement and progression
Store dated class placements by academic period, preserving history. Validate duplicate active placements and support authorised exceptions with audit. Handle stage transition and transfer as explicit events.

### FR-05 Attendance
Record attendance by configured date/session for assigned learners. Candidate statuses (present, unexplained absence, excused absence, late) remain subject to school/policy validation. Prevent duplicates; corrections require authority, reason and audit. Offline capture is not a release commitment until the offline acceptance gate passes.

### FR-06 Curriculum and assessment configuration
Support versioned curriculum frameworks and sources; grade/subject-specific content standards, performance standards, benchmarks and assessment tasks; local/school standards clearly distinguished from national standards. Support varied methods such as observation, work sample, project, presentation, practical task, quiz and written test. Capture criteria/rubrics, evidence reference, date and teacher. Numeric score is optional. Curriculum terminology and editions must retain source provenance.

### FR-07 Results and achievement
Record learner achievement against configured standards/criteria, teacher judgement/descriptor, feedback and optional numeric score. Do not hard-code unverified scales, weighting, pass/fail or promotion rules. Distinguish missing evidence from zero. Preserve correction history.

### FR-08 Report cards
Provide configurable report sections. Candidate sections include student/school identity, period, outcomes/standards achieved, standards currently being worked towards, subject achievement/evidence, approved attitudes/values fields, attendance, teacher/head teacher comments and authorised sign-off. Mark each section's evidence class (national instrument, local requirement, optional school configuration, unresolved) in the requirements traceability. Exact template remains subject to current policy and school validation.

### FR-09 Operational reports
Register/class lists, attendance registers and summaries, individual attendance history, assessment recording sheets and class/grade achievement summaries. SAPS/SASS-style layouts are examples only until current use is confirmed.

### FR-10 Import/export
Controlled, previewable import/export with row validation, duplicate detection and no silent overwrite.

### FR-11 User administration
Individual accounts, prompt revocation, school-scoped roles and class/subject permissions.

### FR-12 Audit and history
Audit important academic, administrative, security, export and report events with actor, timestamp, action, affected record and reason where applicable.

### FR-13 Offline and synchronisation
Offline attendance/assessment capture is a target only. Specify protected local storage, device/session binding, minimal cache, queued writes, unique operation IDs, idempotency, retries, conflict handling, sync status, logout/cache clearing, lost-device response and recovery. Release acceptance requires end-to-end tests for intermittent connectivity, power/device loss, shared-device handover, concurrent edits, account revocation and no silent data loss. If the gate is not passed, ship online-only and explicitly defer offline.

## 4. Non-functional requirements

Privacy by design; server-side least privilege; school isolation; encrypted transport; audit; low-bandwidth mobile usability; accessible forms; measurable performance targets; tested backup/restore; data portability; maintainable migrations and automated tests. Shared phones, power interruption, low/no connectivity and printing must be considered in field validation.

## 5. Evidence classification and traceability

Every requirement and report field must be classified as one of:
- National requirement (current authoritative source confirmed).
- Official curriculum/policy guidance (source and status recorded).
- Teacher-guide example.
- Provincial/district instruction.
- School-specific practice.
- Proposed product feature.
- Unresolved.

The evidence register must cite source, issuer, version/date, retrieval date, page/section and confidence. PRD wording must not present an illustrative or local practice as a national mandate.

## 6. MVP boundaries

Included: school setup, users/roles, academic structure, enrolment, placements, attendance, curriculum-aware assessment/evidence/results, configurable reports, export, audit and operational safeguards. Excluded: elementary module, staff management, payroll, assets, fees, parent/student portal, library, transport, advanced analytics and national platform implementation.

## 7. Business rules requiring validation

Academic calendar; subject/syllabus versions; class group and grade assignment; standards and benchmarks; attendance definitions/calculations; report fields/sign-off; student identifiers/transfers; retention; grading descriptors and progression. No unresolved rule becomes an official PNG requirement by assumption.
