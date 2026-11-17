# Product Requirements — Release 1 MVP

**Document:** PRD-001 | **Version:** 0.1 | **Status:** Draft for review

## 1. Product outcome

A school can maintain a trusted digital student register and use teacher-entered attendance and assessment data to produce accurate academic reports.

## 2. Personas

- **Head teacher / school administrator:** configures the school, academic periods, users, grades/classes and reporting; oversees records.
- **Class teacher:** manages assigned class register, attendance and relevant assessment records.
- **Subject teacher:** records assessments/results for authorised classes and subjects.
- **Read-only report viewer:** accesses only explicitly authorised reports.

A user may hold more than one role in a small school. Permissions must be additive only where explicitly assigned and must remain school-scoped.

## 3. Functional requirements

### FR-01 School setup
Maintain school name, approved school identifier (if available), location, contact details, logo and configuration. Do not invent official identifiers. School settings are isolated from other deployments.

### FR-02 Academic structure
Configure academic years, terms/periods, grades (including the common Grades 1–8 range where applicable), classes/streams, subjects and teacher assignments. Do not assume every school offers every grade or has multiple streams.

### FR-03 Student register and enrolment
Create, view, search and update student profiles. Proposed fields include school student number, legal/preferred names, date of birth where known, sex where required, guardian/contact details, village/community and enrolment details. Collect only necessary information. Support active, transferred, withdrawn and completed statuses. Preserve history; do not hard-delete enrolled learner records through normal workflows.

### FR-04 Class placement and progression
Record dated placement of a student in a class for an academic period. Support promotion and class changes without overwriting historical class membership. Prevent duplicate active placement conflicts unless an authorised exception is recorded.

### FR-05 Attendance
Allow authorised teachers to view an assigned class list and record attendance by date and session as configured. Initial statuses to validate: present, absent, late and excused/approved absence. Prevent duplicate attendance entries for the same student/date/session. Permit corrections only to authorised users, recording who changed what, when and why. Support offline capture only after the sync design is validated.

### FR-06 Assessment configuration
Allow authorised staff to configure assessment name/type, subject, class, academic year, term, date, maximum score and applicable weighting (if approved). Assessment types are configurable; examples include classwork, assignment, test and examination.

### FR-07 Results
Enter and edit learner scores within permitted limits. Validate score against maximum score, required student/class/subject/period relationships and duplicate entries. Preserve change history. Do not impose an unvalidated grading scale or automatic pass/fail rule.

### FR-08 Report cards
Generate a student report for a selected student, class, academic year and reporting period. Include school identity, student identity, grade/class, subject results, configured grades/marks, attendance summary, teacher comments and head teacher comments/signature areas where approved. Clearly distinguish missing results from zero marks. Support preview, print and PDF output.

### FR-09 Operational reports
Provide student register/class list, daily and period attendance summaries, individual attendance history, assessment/result sheets and class/grade performance summaries. Reports must show their period, filters and generation date.

### FR-10 Import/export
Provide controlled CSV export of school-owned records and documented import templates. Imports must validate rows, report errors and avoid silent duplicates. Bulk imports must be previewable before committing.

### FR-11 User administration
Create/disable accounts, assign school-scoped roles and class/subject permissions, and revoke access promptly. No shared teacher accounts.

### FR-12 Audit and record history
Record security-relevant and important academic changes, including actor, timestamp, action and affected record. Audit data must not be editable by ordinary users.

### FR-13 Offline and synchronisation
The intended design is to support offline attendance and assessment capture on authorised devices. Before release, specify local storage protection, device/user binding, queued writes, retry/idempotency, conflict detection, sync status and recovery after device loss. Do not claim offline support until end-to-end tests pass.

## 4. Non-functional requirements

- **Privacy:** collect the minimum necessary learner information; document purpose, access, retention and disclosure.
- **Security:** secure authentication, least privilege, school isolation, encrypted transport, protected secrets and audit trail.
- **Reliability:** validated backup and restoration; no silent data loss.
- **Usability:** mobile-first, low-bandwidth conscious, simple class-register workflow and clear validation messages.
- **Accessibility:** readable text, adequate contrast, keyboard support and clear labels.
- **Performance:** define measurable targets in the test plan using realistic school-sized datasets and low-bandwidth conditions.
- **Maintainability:** modular code, migrations, automated tests and deployment documentation.
- **Portability:** documented exports and stable identifiers.
- **Interoperability:** versioned API and mapping layer; no dependency on an unconfirmed national platform.

## 5. MVP boundaries

Included: school setup, users/roles, academic structure, enrolment, class placement, attendance, assessments/results, report cards, essential reports, export, audit and operational safeguards.

Excluded: staff management, payroll, assets/equipment, fees, parent/student portal, library, transport, advanced analytics and national platform build.

## 6. Business rules requiring validation

- Academic calendar and term count.
- Applicable grades and subject names/codes.
- Assessment methods and score aggregation.
- Grading bands, descriptors and progression rules.
- Attendance definitions and reporting denominator.
- Required report-card fields and sign-off.
- Student identity and transfer process.
- Data retention and correction rules.

No rule in this list becomes an official PNG requirement until supported by an authoritative source or explicit school policy.

## 7. Traceability

Every requirement must map to one or more GitHub Issues, implementation evidence and acceptance tests. Scope changes require impact assessment and approval.
