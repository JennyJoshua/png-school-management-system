# Reporting Requirements — Release 1

**Document:** REP-001 | **Version:** 0.2 | **Status:** Draft; PNG and school policy validation required

## 1. Purpose

Use trusted enrolment, attendance and assessment records to generate useful teacher and head-teacher reports. Report layouts must be configurable because schools may have different approved formats and communities must be able to understand the reports.

## 2. MVP report catalogue

1. Student enrolment register.
2. Class/grade list.
3. Daily attendance register.
4. Monthly/term attendance summary.
5. Individual student attendance history.
6. Assessment recording sheet / class mark sheet.
7. Individual student report card.
8. Class/grade achievement summary.
9. School-level enrolment and attendance summary.
10. Configurable export or print view of a student assessment profile.

## 3. Student report card — proposed configurable sections

- School name, verified school identifier (if applicable), location and logo.
- Academic year, reporting period and student identity.
- Grade/class and class teacher.
- Learning outcomes achieved since the previous report.
- Learning outcomes the student is currently working towards.
- Subject/learning-area achievement, criteria and evidence summary.
- Marks, maximum marks and configured achievement descriptor where the school's approved scheme uses them.
- Attitudes, values and other approved student-specific information.
- Attendance counts with defined categories.
- Teacher and head teacher comments.
- Approved student, parent/guardian and teacher sign-off fields where school practice requires them.
- Date generated and report-template version.

These sections reflect the Department of Education's National Assessment and Reporting Policy (2003), section 5.3.1, and the Grade 6 English Teacher Guide (2019), sample report card pages 125–126. They are source-backed examples, not a claim that the sample is the current mandatory form for every primary school. Validate current policy, later circulars and school practice before fixing a production template.

## 4. Accuracy rules

- Missing result is not the same as zero.
- Every report identifies its period and generation date.
- Attendance percentages must disclose the denominator and treatment of excused absences.
- Do not calculate an overall score until aggregation and weighting rules are approved.
- Support evidence-based achievement reporting; do not reduce all assessment to written tests or numeric marks.
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

The research register at [PNG Curriculum and Assessment Research](../research/PNG_CURRICULUM_ASSESSMENT_RESEARCH.md) records the source evidence and limitations. Before finalising the report card, validate the current national policy and applicable curriculum documents with the pilot school. Record source title, issuing authority, date/version, relevant page/section and exact requirement. Distinguish national requirements from school-specific practice.

## 7. Later reporting

Future releases may add staff returns, asset/inventory reports, advanced performance analysis and national statistical returns. These are not part of the Release 1 acceptance scope.
