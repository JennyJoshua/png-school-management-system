# Reporting Requirements — Release 1

**Document:** REP-001 | **Version:** 0.3 | **Status:** Draft; current PNG and school validation required

## 1. Purpose

Generate accurate, understandable reports from validated enrolment, attendance and assessment records. Templates and configurable fields must reflect each school's approved practice without misrepresenting local examples as national rules.

## 2. MVP report catalogue (proposed)

1. Student enrolment register.
2. Class/grade list, including mixed-grade class grouping.
3. Daily attendance register.
4. Period attendance summary and individual attendance history.
5. Assessment recording sheet.
6. Individual student report card.
7. Class/grade achievement summary.
8. School enrolment and attendance summary.
9. Controlled student assessment profile export.

## 3. Report-card sections and evidence status

Candidate sections:
- School/student identity, academic period, grade and class.
- Curriculum content/performance standards and benchmarks relevant to the student's grade and subject.
- Learning outcomes/standards achieved and those currently being worked towards.
- Subject achievement, criteria and evidence summary.
- Marks/descriptors only where the approved scheme uses them.
- Attitudes, values and other student-specific information only where approved and appropriately defined.
- Attendance with explicit categories and calculation rules.
- Teacher/head teacher comments and school-approved sign-off fields.
- Generation date and template version.

The 2003 National Assessment and Reporting Policy PDF describes achieved and developing outcomes and student-specific information. The Grade 6 English Teacher Guide (2019) provides a sample layout. Until current policy status and local requirements are confirmed, classify these as **published policy evidence requiring current-status confirmation** and **illustrative guide example**, not as a definitive current mandatory national template.

## 4. Accuracy and integrity rules

- Missing result is not zero.
- Every report identifies period, filters, generation date and template version.
- Attendance rates show denominator and treatment of excused absence/late categories.
- No aggregate score, grade band or pass/fail rule without an approved scheme.
- Incomplete or unavailable data is shown explicitly.
- Report generation does not modify source records.
- Reissued reports preserve prior issue history where formally issued.
- A mixed-grade class report must use each learner's applicable grade/curriculum, not the class label alone.

## 5. Output and field constraints

Mobile preview; print-friendly black-and-white layout; PDF; authorised CSV export. Validate printing access, paper workflow, power interruptions, shared device use and whether paper registers remain the official record during pilot. Signatures and letterheads must not be captured or published without explicit authority and redaction.

## 6. Validation gates

Before fixing a production report:
- Confirm current national/provincial instrument, edition and exact required fields with the competent authority.
- Compare blank/de-identified school templates and actual teacher/head-teacher workflow.
- Obtain teacher validation and documented approval from the responsible school authority.
- Where a field is claimed as national/provincial, cross-check with a second school or competent provincial/district office.
- Record unresolved conflicts; keep the field configurable or omit it from fixed defaults.

Research evidence and limitations are maintained in [RES-001](../research/PNG_CURRICULUM_ASSESSMENT_RESEARCH.md).
