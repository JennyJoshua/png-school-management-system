# Project Charter — PNG School Management System

**Document:** PC-001  
**Version:** 0.2 (Draft)  
**Status:** Proposed baseline — owner approval required  
**Product:** PNG School Management System (PNG-SMS)

## 1. Purpose

Build a reusable school-management product for Papua New Guinea (PNG), beginning with primary schools. Each school should be able to operate its own application and central database independently. The product will be delivered in controlled releases, with a practical MVP before broader administration or national integration is attempted.

## 2. Vision

Give PNG primary schools a dependable, accessible way to maintain core student and academic records and produce useful school reports. Establish common data standards and integration interfaces so that participating schools can exchange authorised data with a future national platform if one becomes available and is approved.

## 3. Initial users and pilot

- Initial market: PNG primary schools (Grades 3–8 under the Department of Education's published primary education structure).
- Elementary Prep–Grade 2 is a separate education stage and is outside the initial primary-school MVP unless the owner approves a scope change.
- Proposed reference/pilot school: Baimuru Primary School, subject to school-owner approval, data permissions and pilot readiness.
- Primary users: head teacher/school administrator, class teacher and authorised subject teacher.
- Parents and students do not require accounts in Release 1.

Use synthetic or properly de-identified data during development. Real learner data may only be used for a pilot after appropriate school authority, consent/notice, security and operational safeguards are in place.

## 4. Release 1 objective

Deliver a usable MVP that supports:
1. School profile and configuration.
2. User accounts and role-based access.
3. Grades 3–8 (only grades actually offered by the school), classes/streams and configurable academic year/term setup.
4. Student enrolment and student register.
5. Daily attendance, including correction history.
6. Assessment evidence and student achievement/results.
7. Individual student report cards.
8. Essential class and school reports, export and print/PDF.
9. Auditability, backup and recovery, and a tested deployment process.

## 5. Explicit exclusions from Release 1

- Elementary Prep–Grade 2.
- Staff personnel/payroll and staff attendance.
- Equipment, inventory, asset and maintenance management.
- Parent/student portals and messaging.
- Fees, accounting, payments and procurement.
- Timetable, library and transport modules.
- National platform implementation or automatic nationwide data sharing.
- Advanced predictive analytics.
- Native Android/iOS applications (PWA is the proposed first client).

These may be considered in later releases through separately approved requirements.

## 6. Product and deployment principles

- Reusable application code, independently configured/deployed for each school.
- Separate school database per deployment as the current preferred model; confirm operational cost, backup and maintenance implications in architecture validation.
- No cross-school access by ordinary school users.
- Stable school and student identifiers, common code lists and documented APIs.
- Configurable grades, classes, subjects, terms, assessment methods and report templates.
- Assessment records should be capable of representing learning outcomes/standards, criteria, evidence and teacher judgements as well as numeric scores.
- Mobile-first design and offline-first workflows for attendance and assessment, with explicit sync/conflict handling.
- Exportable school-owned data and documented recovery procedures.
- Modular design: later features must not require a rewrite of the MVP core.

## 7. Success measures

Release 1 is successful when a pilot school can independently:
- Set up its academic year, grades and classes.
- Enrol and find students, preserving historical records.
- Record and review daily attendance.
- Record a range of assessment evidence and enter results/achievement judgements.
- Generate accurate, printable student report cards and class summaries.
- Use the supported offline workflows and synchronise without silent data loss.
- Restore from a tested backup.
- Demonstrate that users cannot access records outside their authority.

Quantitative performance targets and pilot duration will be set in the approved test plan.

## 8. Constraints and assumptions

- Android phones are a primary access device; desktop/tablet support remains useful.
- Connectivity may be intermittent or unavailable.
- Schools may have different class structures, assessment practices and report formats.
- PNG Department of Education curriculum and assessment material is the starting evidence base. Its current applicability, updates and school-level implementation must be validated; no single grading scale or official form is assumed.
- Free-tier services may have limits and are not automatically suitable for production. No paid service or upgrade without explicit approval.
- The national platform and its technical standards are unknown; integration readiness must use adaptable mappings, not speculative hard-coded interfaces.

## 9. Governance and approval gates

The owner approves the product baseline, material scope changes, main-branch merges where required, production deployment, paid services/upgrades, destructive actions and hosted database migrations. Routine implementation and testing within an approved scope may proceed through the agreed workflow.

GitHub Issues is the authoritative implementation backlog and handover register. Decisions and changes must be recorded in repository documentation or linked issues.

## 10. Phase 0 exit conditions

Before implementation:
- Product requirements and MVP boundaries approved.
- PNG curriculum/reporting assumptions researched and gaps recorded.
- Data dictionary and database model reviewed.
- Architecture, school isolation and offline/sync design reviewed.
- Privacy, security, backup and recovery plan reviewed.
- MVP acceptance criteria and test strategy approved.
- Repository backlog prioritised and delivery checks defined.

## 11. Open decisions

1. Confirm school-by-school separate database versus another isolation pattern after cost/operations analysis.
2. Confirm academic year/term structure and whether schools can configure multiple terms.
3. Validate grade, subject, assessment and reporting conventions against current applicable PNG requirements and school practice.
4. Define student identifier policy and transfer/migration process.
5. Define exact offline scope and conflict-resolution rules.
6. Confirm hosting region, data residency expectations, backup retention and operating costs.
7. Confirm pilot authority, data governance and real-data safeguards.
8. Confirm how standards/outcomes, evidence, rubrics/descriptors and achievement judgements are represented in the MVP.

**Approval:** This is a draft charter. It does not authorise production implementation, real learner-data processing or paid infrastructure.
