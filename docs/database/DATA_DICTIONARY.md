# Release 1 Data Dictionary and Conceptual Data Model

**Document:** DD-001 | **Version:** 0.1 | **Status:** Conceptual draft — not a physical schema  
**Scope:** Primary-school MVP (Grades 3–8); no production database or migration authorised.

## 1. Purpose and rules

This document defines the minimum conceptual information needed to support Release 1. It is technology-neutral. Field types are logical descriptions, not PostgreSQL column definitions. Final mandatory fields, retention periods, identifiers and code values require school and competent-authority validation.

- Internal immutable identifiers are system-generated; do not use names as keys.
- Every school-owned record is scoped to one school boundary, even if the first architecture uses one database per school.
- Keep student grade enrolment, class-group membership, curriculum grade and subject/standard assignment distinct to support mixed-grade teaching.
- Preserve effective-dated history; normal user workflows do not hard-delete academic records.
- Store provenance and version for curriculum standards, assessment judgements and report templates.
- Collect the minimum necessary personal information. Guardian contact is optional and restricted until purpose/authority is validated.
- Distinguish unknown, not assessed, absent, pending and zero.
- No national identifier is assumed. Any external identifier requires an authoritative scheme and lawful purpose.
- Retention and disposal must be configured only after policy/legal validation.

## 2. Sensitivity classes

| Class | Meaning | Handling |
|---|---|---|
| Public | Approved public school/product information | May be published after review |
| Internal | Operational configuration without personal data | Authenticated school access |
| Personal | Learner/staff identity or contact information | Least privilege, purpose limitation, access audit |
| Sensitive personal | Data that could cause greater harm if exposed (e.g. safeguarding/health notes, if ever approved) | Excluded from MVP unless separately justified and approved; stricter access |
| Security | Credentials, tokens, audit/security events | Never expose secrets; restricted administration |

## 3. Conceptual entities

### 3.1 School and access

| Entity | Key attributes (logical) | Relationships / rules | Sensitivity |
|---|---|---|---|
| School | internal ID; verified school code (optional); name; location; contact; timezone; configuration | Owns all school records; official identifiers require source verification | Internal/Personal |
| User account | auth subject ID; status; created/disabled timestamps | One person per account; authentication provider owns credentials | Personal/Security |
| School membership | user ID; school ID; membership status; start/end | Binds an account to a school; supports revocation | Personal |
| Role assignment | membership ID; role; scope; effective dates; granted-by | Roles: administrator, class teacher, subject teacher, report viewer; least privilege | Security |
| Audit event | actor; timestamp; action; record reference; reason; outcome; correlation ID | Append-only application event; restricted access | Security/Personal |

### 3.2 Academic structure

| Entity | Key attributes (logical) | Relationships / rules | Sensitivity |
|---|---|---|---|
| Academic year | school; label; start/end dates; status | Parent of academic periods | Internal |
| Academic period | year; period label/type; start/end; reporting status | Terms/reporting periods belong to a year; exact calendar configurable | Internal |
| Grade level | code; display label; stage; sequence; active dates | Grade 3–8 primary defaults; Prep–2 excluded unless approved | Internal |
| Class group | school; year; label; stream; class teacher; status | Teaching group may contain learners from multiple grade levels | Personal/Internal |
| Class membership | learner; class group; effective dates; membership status | Dated membership; does not define or overwrite learner's grade | Personal |
| Subject | code; name; active dates; source/version | Grade/period availability is configurable; no assumed universal subject list | Internal |
| Teacher assignment | user/membership; class group; subject; period; effective dates | Assignment scoped to school and period; authorises relevant actions | Personal/Security |

### 3.3 Learner and enrolment

| Entity | Key attributes (logical) | Relationships / rules | Sensitivity |
|---|---|---|---|
| Student | internal ID; school-local student number; minimum approved identity fields; status | Student number unique within school; names are not keys | Personal |
| Enrolment | student; admission date; entry type; status; exit date/reason; source | Multiple historical enrolments/transfers possible; preserve history | Personal |
| Grade enrolment | student; academic year/period; grade; effective dates; status | Records learner's grade independently from class group | Personal |
| Placement | student; class group; effective dates; reason; authorised-by | Dated placement; overlapping active placements require explicit exception | Personal |
| Guardian contact (optional) | student; contact name; relationship; contact method; purpose/consent status | Collect only when approved; restricted role access; not required for MVP until validated | Personal |

### 3.4 Curriculum and assessment

| Entity | Key attributes (logical) | Relationships / rules | Sensitivity |
|---|---|---|---|
| Curriculum framework | name; issuer; version; effective dates; source URL/document reference | Versioned; preserve historical framework | Internal |
| Curriculum standard | framework; grade; subject; standard type; code; statement; source page | Distinguish content standard, performance standard, benchmark and local standard | Internal |
| Assessment activity | class/subject/period; framework version; method; title; date; creator; status | Methods may include observation, work sample, project, practical, presentation, quiz or written test | Internal/Personal |
| Assessment criterion | activity/standard; criterion; rubric/descriptors; version | Descriptors are configurable and source-backed | Internal |
| Evidence reference | assessment; student; evidence type; description/reference; collected date; recorded-by | Prefer metadata/reference over uploading identifiable evidence files; any file support needs separate privacy/security approval | Personal |
| Achievement judgement | student; criterion/standard; judgement/descriptor; feedback; assessed date; teacher; status | Numeric score optional; missing evidence distinct from zero; correction history retained | Personal |
| Numeric score (optional) | judgement/activity; score; maximum; scale/source | Only when an approved assessment scheme defines its meaning and bounds | Personal |

### 3.5 Attendance and reporting

| Entity | Key attributes (logical) | Relationships / rules | Sensitivity |
|---|---|---|---|
| Attendance session | class group; date; session label; period; created-by; status | One configured session for a class/date; calendar and session rules configurable | Internal |
| Attendance record | student; session; status; recorded-by; recorded-at; correction reason | Unique learner/session; categories and excused/late rules require validation | Personal |
| Report template | school; template name; version; effective dates; approval record | Configurable sections; versioned; approved by responsible authority | Internal |
| Report issue | student; period; template version; generated-at; generated-by; issue status | Reissue history retained; source records unchanged | Personal |
| Report section/value | report issue; section key; rendered value/source references | Missing/unavailable values shown explicitly; no unapproved grading calculations | Personal |
| Export job | actor; scope; filters; purpose; generated-at; result; file reference/expiry | Preview, authorisation and audit; minimise exported fields | Security/Personal |

### 3.6 Offline and synchronisation (conditional)

| Entity | Key attributes (logical) | Relationships / rules | Sensitivity |
|---|---|---|---|
| Registered device/session | user; device/session identifier; registration/revocation timestamps | Only if offline scope approved; no unnecessary device fingerprinting | Security |
| Sync operation | unique operation ID; actor/device/session; entity reference; operation type; client/server timestamps; status | Idempotent retries; server validates authority and data state | Security/Personal |
| Sync conflict | operation; server/client version references; conflict type; resolution; resolver; timestamp | Visible and auditable; no silent last-write-wins for academic records | Security/Personal |

## 4. Relationship rules

- School → memberships, academic years, learners, classes, curriculum configuration and reports.
- Academic year → periods; grade enrolment and class groups are dated within academic periods.
- Class group ↔ learners through dated class membership; class group is not a substitute for learner grade.
- Learner → enrolments, grade enrolments, placements, attendance, evidence, judgements and report issues.
- Curriculum framework → standards; assessment activities reference the exact applicable framework/standard version.
- Assessment activity → criteria; learner evidence and achievement judgements reference activity/criterion.
- Attendance session → one attendance record per learner per session.
- Report issue → versioned template and period-specific source records.
- User/membership → scoped role assignments, teacher assignments and audit events.

## 5. Candidate validation and constraints

1. School-local student number uniqueness and format.
2. Required admission/identity fields and acceptable evidence.
3. Transfer, withdrawal, re-enrolment and retention rules.
4. Grade enrolment and class membership date boundaries.
5. Mixed-grade class/subject allocation.
6. Attendance categories, session structure, correction authority and calculation.
7. Curriculum version/effective-date mapping and benchmark source.
8. Evidence storage, file types, retention and access (file upload excluded pending separate approval).
9. Achievement descriptor, optional score and report calculations.
10. Guardian contact purpose, access and consent/notice.
11. Audit retention, export permissions and report reissue.
12. School timezone, academic calendar and timestamp handling.

## 6. Deliberately excluded from this draft

Physical SQL types, table names, indexes, constraints implementation, RLS policies, API payloads, migration scripts, production seed data, grading bands, promotion algorithms, national student identifier, safeguarding/health fields, payroll, assets, fees, parent portal and national platform integration.

## 7. Review and approval

This dictionary is a draft for requirements and workflow review. It is not a production schema. Approval requires traceability to the approved PRD, teacher and responsible school-authority validation, privacy review and architecture/security review. Any field not justified by a validated purpose must be removed or deferred.
