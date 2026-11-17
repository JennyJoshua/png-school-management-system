# Reporting Requirements — Release 1

**Document:** REP-001 | **Version:** 0.1 | **Status:** Draft; PNG and school policy validation required

## 1. Purpose

Use trusted enrolment, attendance and assessment records to generate useful teacher and head-teacher reports. Report layouts must be configurable because schools may have different approved formats.

## 2. MVP report catalogue

1. Student enrolment register.
2. Class/grade list.
3. Daily attendance register.
4. Monthly/term attendance summary.
5. Individual student attendance history.
6. Assessment mark sheet.
7. Individual student report card.
8. Class/grade assessment summary.
9. School-level enrolment and attendance summary.

## 3. Student report card — proposed fields

- School name, verified school identifier (if applicable), location and logo.
- Academic year and reporting period.
- Student name and school student number.
- Grade/class and class teacher.
- Subject names and assessment/result summary.
- Marks, maximum marks and configured grade/descriptor where approved.
- Attendance counts and clearly defined attendance rate.
- Teacher comment.
- Head teacher comment and sign-off area.
- Date generated and report-template version.

Only include fields that the school has approved and that applicable requirements support. No grading bands, weighting, pass/fail thresholds or official wording are assumed in this draft.

## 4. Accuracy rules

- Missing result is not the same as zero.
- Every report identifies its period and generation date.
- Attendance percentages must disclose the denominator and treatment of excused absences.
- Do not calculate an overall score until aggregation and weighting rules are approved.
- Report generation must not modify source academic records.
- Corrections after a report is generated must be reflected in a newly generated version; preserve an audit trail where reports are formally issued.
- Show incomplete data clearly rather than silently omitting it.

## 5. Output and usability

- Mobile preview.
- Print-friendly layout.
- Downloadable PDF.
- School logo and configurable header/footer.
- Readable black-and-white printing.
- Consistent pagination and no clipped learner names or subjects.
- CSV export for authorised data users, with privacy safeguards.

## 6. PNG requirements validation

Before finalising the report card, research applicable PNG primary curriculum, assessment and reporting guidance from authoritative education sources and validate the proposed layout with the pilot school. Record source title, issuing authority, date/version, relevant page/section and exact requirement. Distinguish national requirements from school-specific practice.

## 7. Later reporting

Future releases may add staff returns, asset/inventory reports, advanced performance analysis and national statistical returns. These are not part of the Release 1 acceptance scope.
