# Release 1 Requirements Traceability Register

**Document:** RT-001 | **Version:** 0.1 | **Status:** Draft — evidence and school validation incomplete

This register links product requirements to conceptual data domains, acceptance evidence and unresolved decisions. It does not certify national or provincial requirements.

| Requirement | Scope | Conceptual data domains | Evidence / validation status | Acceptance evidence |
|---|---|---|---|---|
| FR-01 School setup | School profile and configuration | School | Product capability; official identifiers must be verified | School configuration test; identifier provenance |
| FR-02 Academic structure | Grades 3–8, mixed-grade class groups, periods, subjects | Academic year, period, grade, class group, membership, subject | Current DoE public SBC resources; local structure still to validate | Mixed-grade fixture with distinct learner grades |
| FR-03 Enrolment | Minimum learner record and lifecycle | Student, enrolment, grade enrolment | Required fields and retention unresolved | Create/update/transfer/withdrawal history tests |
| FR-04 Placement | Dated class membership and progression | Class membership, placement | School workflow validation pending | Historical placement and overlap tests |
| FR-05 Attendance | Session register and corrections | Attendance session, attendance record, audit | Categories and calculations unresolved | Duplicate prevention, correction authority and calculation tests |
| FR-06 Curriculum/assessment | Versioned standards, varied methods and evidence | Framework, standard, activity, criterion, evidence | Current SBC syllabus evidence; grade/subject editions and local practice to verify | Source-version trace and varied-method tests |
| FR-07 Achievement | Judgement/descriptor; optional numeric score | Achievement judgement, optional score | No grading scale approved | Missing vs zero; descriptor and score validation |
| FR-08 Report cards | Configurable sections and sign-off | Template, report issue, report value | Historical policy and guide example; current status/local requirements unresolved | Approved template, field provenance and print tests |
| FR-09 Operational reports | Register, attendance, assessment reports | Student, class, attendance, assessment | Product scope; sample layouts not assumed mandatory | Report catalogue tests |
| FR-10 Import/export | Controlled data exchange | Export job and referenced records | Product capability; transfer format unresolved | Preview, validation, audit and round-trip tests |
| FR-11 User administration | Individual accounts and scoped roles | User, membership, role, teacher assignment | Security design pending | Permission matrix and revocation tests |
| FR-12 Audit/history | Traceable changes | Audit event | Product/security requirement | Audit coverage and tamper/access tests |
| FR-13 Offline/sync | Conditional Release 1 capability | Device/session, sync operation/conflict | Target only; may be deferred | End-to-end offline gate; online-only fallback |

## Evidence classification

- **Current official curriculum resource:** Department of Education public SBC page and syllabus; authoritative for the published curriculum resource, not necessarily every local implementation detail.
- **Published policy with current status unresolved:** National Assessment and Reporting Policy PDF; do not assert current legal force until confirmed.
- **Teacher-guide example:** illustrative only; not a national mandate.
- **School/provincial practice:** must be validated with authorised source and scope.
- **Product proposal:** design choice, not an external requirement.
- **Unresolved:** no implementation rule until confirmed or explicitly accepted as configurable product behaviour.

## Open validation items

1. Current mandatory enrolment, transfer and student-record fields.
2. Attendance status definitions and calculation.
3. Current reporting policy status, report card requirements and sign-off.
4. Grade/subject syllabus editions and effective dates.
5. Data retention, correction and deletion requirements.
6. Guardian contact purpose and access.
7. Teacher and responsible school-authority workflow sign-off.
8. Second-school or competent provincial/district cross-check for any claimed national/provincial practice.
