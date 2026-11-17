# Database Design — Initial Logical Model

**Document:** DB-001 | **Version:** 0.1 | **Status:** Conceptual draft; migration prohibited until approved

## 1. Principles

- One database per school is the preferred deployment pattern, subject to architecture/cost validation.
- Use PostgreSQL relational integrity, foreign keys, constraints and transactions.
- Use stable UUID primary keys; maintain a separate human-readable school student number.
- Preserve academic history rather than overwriting past class placements or results.
- Store dates and timestamps consistently; define the school timezone.
- Use controlled code tables/configuration rather than hardcoding school-specific labels.
- Record created/updated metadata and audit important changes.
- Avoid collecting sensitive personal data unless a validated school purpose requires it.

## 2. Proposed logical entities

| Entity | Purpose / key relationships |
|---|---|
| school_profile | Name, school identifier if verified, location and configuration |
| user_profile | Authenticated user mapped to school-specific role/profile |
| role / permission | Administrator, class teacher, subject teacher, report viewer |
| academic_year | School academic year |
| academic_period | Term or reporting period within an academic year |
| grade | Configurable grade level |
| class_group | Class/stream within a grade and year |
| subject | School subject and optional standard code |
| teacher_assignment | User/teacher assigned to class/subject/period |
| student | Stable learner identity within this school database |
| guardian_contact | Necessary parent/guardian contacts, with access restrictions |
| enrolment | Admission date, status, entry details and exit/transfer details |
| student_class_placement | Dated student-to-class relationship for each period |
| attendance_session | Date, class and configured session |
| attendance_record | Student status for a session; unique constraint prevents duplicates |
| assessment | Subject/class/period assessment definition and maximum score |
| student_result | Student score and comments for an assessment |
| report_template | Versioned school-approved report layout/configuration |
| audit_event | Actor, action, entity, timestamp and change metadata |
| sync_operation (if offline) | Idempotent client operation, status and conflict metadata |

## 3. Relationship outline

```text
academic_year -> academic_period
grade -> class_group -> student_class_placement -> student
student -> enrolment
class_group -> teacher_assignment
class_group + subject + academic_period -> assessment
assessment + student -> student_result
class_group + date/session -> attendance_session
attendance_session + student -> attendance_record
student + academic_period -> report card data
user_profile -> audit_event
```

## 4. Key constraints and rules

- Student number is unique within a school deployment; never use a name as a key.
- Preserve former enrolments and class placements with effective dates/status.
- A student must not have overlapping active class placements for the same applicable period unless an authorised exception is modelled.
- Attendance has a unique key for student + session.
- Result has a unique key for student + assessment.
- Score must be non-negative and no greater than the assessment maximum unless a formally defined exception exists.
- Assessment must belong to a valid class, subject and academic period.
- A report must identify the exact academic period and data snapshot/generation time.
- Deactivation/transfer must not cascade-delete academic history.
- Use soft-retirement or status transitions for core records; hard deletion is restricted.

## 5. Identity and future transfers

Use internal UUIDs as immutable database keys. A student number is school-scoped and may not be globally unique. National student identifiers must remain nullable and must only be added when an authoritative scheme and lawful use are confirmed.

Design an export package that includes school identifier, record identifiers, data dictionary/version, academic period and provenance. A transfer must be authorised, previewed and auditable; it must not expose unrelated student records.

## 6. Security

Apply least-privilege database roles and row-level security where appropriate. Validate school boundary at API and database layers. Do not rely on hidden UI controls. Never expose service-role secrets to the browser. Audit access and sensitive changes according to the approved privacy plan.

## 7. Offline/sync considerations

If offline writes are supported, each client mutation needs a globally unique operation ID, device/session context, client timestamp and server receipt timestamp. Server validation remains authoritative. Duplicate retries must not create duplicate records. Conflicts must be visible and resolvable; preserve both versions where required for review.

## 8. Not yet specified

Exact column types, nullability, indexes, enum/code values, retention rules, RLS policies, migration scripts, seed data and backup settings are not final. They require a reviewed data dictionary and approved technical design before migrations are created or applied.
