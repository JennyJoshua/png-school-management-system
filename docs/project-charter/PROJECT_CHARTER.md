# Project Charter — PNG School Management System

**Document:** PC-001  
**Version:** 0.3 (Draft)  
**Status:** Proposed baseline — owner and relevant school authority approval required  
**Product:** PNG School Management System (PNG-SMS)

## 1. Purpose

Build a reusable school-management product for Papua New Guinea (PNG), beginning with primary schools. Each school should be able to operate its own application and central database independently. Delivery is phased, beginning with a carefully bounded MVP.

## 2. Vision

Help PNG primary schools maintain dependable student and academic records and produce useful school reports. Establish adaptable data standards and integration interfaces for possible future authorised exchange with a national platform.

## 3. Initial users and pilot

- Initial market: PNG primary schools, generally Grades 3–8 under the Department of Education's published structure and current primary curriculum resources.
- Prep–Grade 2 is the elementary stage and is outside the primary MVP. Grade 2 to Grade 3 is an education-stage transition, not an ordinary primary-grade promotion.
- Mixed-grade classes are supported where a school operates them; class composition must not be confused with the student's enrolled grade or curriculum grade.
- Baimuru Primary School is a proposed reference school, not yet an authorised live-data pilot.
- Primary users: head teacher/school administrator, class teacher and authorised subject teacher. Parents and students do not need accounts in Release 1.

Use synthetic or properly de-identified information during discovery and development. Real learner data requires documented approval from the legally/administratively responsible school authority, appropriate notice/consent where required, defined access, security controls and pilot readiness. If the owner is also a school employee, the owner must not be treated as the sole independent school-authority approval where governance rules require another authority. The appropriate school governing authority and relevant district/provincial education authority must be identified and their role documented before a live pilot. Do not assume which body has approval jurisdiction.

## 4. Release 1 objective

Deliver a usable MVP for:
1. School profile and configuration.
2. Individual user accounts and role-based access.
3. Configurable academic year/periods, Grades 3–8 as applicable, mixed-grade class groups, streams, subjects and teacher assignments.
4. Student enrolment/register and dated class placements.
5. Daily attendance with correction history.
6. Standards/outcomes-aware assessment activities, criteria, evidence and achievement/results.
7. Configurable student report cards.
8. Essential class/school reports, controlled export and print/PDF.
9. Auditability, backup/recovery and a tested deployment process.

Offline attendance and assessment capture is a **Release 1 target, not a current promise**. It may be included only if local data protection, device/session binding, queued writes, idempotent retries, conflict handling, sync visibility, lost-device response and recovery pass end-to-end acceptance tests on supported devices. If these tests are not completed, Release 1 must explicitly ship online-only and record offline capture as deferred; no marketing or requirements text may describe it as delivered.

## 5. Explicit exclusions from Release 1

Elementary Prep–Grade 2 as a separate school-stage module; staff personnel/payroll; assets/inventory; parent/student portals; messaging; fees/accounting/payments/procurement; timetable/library/transport; national-platform implementation or automatic nationwide sharing; predictive analytics; native Android/iOS apps.

## 6. Product and deployment principles

- One reusable codebase; no school-specific code forks.
- Separate school application deployment and database is the preferred hypothesis, not a locked architecture decision.
- Compare credible deployment/isolation alternatives and whole-life operating cost at 1, 10 and 50 schools, including application hosting, database, backups, monitoring, maintenance, support, upgrades and recovery.
- Record a decision threshold before selecting a model: no model passes merely because a free tier exists. It must meet isolation, restore, availability, supportability and portability requirements at each scale. If no affordable model meets them, pause scale-out and revise the operating model; do not weaken security to reduce cost.
- No cross-school access by ordinary school users.
- Stable school/student identifiers, versioned APIs, documented code lists and export/import.
- Configurable curriculum versions, grade-aware subjects, assessment methods and report templates.
- Assessment supports content/performance standards, benchmarks, criteria, evidence and teacher judgement, with numeric scores optional.
- Mobile-first, low-bandwidth-conscious design. Offline functionality is conditional on the tests in §4.
- Preserve historical enrolments and placements; normal workflows must not hard-delete enrolled learner records.

## 7. Success measures

A pilot school can independently configure its academic structure; enrol and locate students; preserve placement history; record/review attendance; record varied assessment evidence and judgements; generate accurate printable reports; demonstrate role and school isolation; and restore from a tested backup. Offline use is a success measure only if the offline gate is passed and included in the release scope.

## 8. Constraints and assumptions

Connectivity and power may be intermittent. Devices may be shared. Schools may rely on paper registers and require printing. Mixed-grade classes and local calendar/reporting differences must be supported. Current Department of Education curriculum resources identify SBC; assessment terminology and policy instruments must be checked against current authoritative sources and actual implementation. Free-tier services are not automatically production-suitable. No paid service or upgrade without explicit approval.

## 9. Governance and approval

The owner approves product baseline, material scope/architecture changes, main merges where the project gate applies, production deployments, paid services/upgrades, destructive actions and hosted database migrations. Routine work within approved scope may proceed under the AI-ACD workflow.

The charter remains Draft until an approval record is committed through a reviewed pull request and explicitly records: approving person/role, authority basis, exact document version and commit, decision date, scope approved, conditions and linked evidence. A GitHub issue checkbox or an undocumented verbal assumption does not change the document's status. The pilot authority and real-data permission are separate approvals from product-owner approval.

GitHub Issues is the authoritative backlog and handover register.

## 10. Phase 0 exit conditions

Requirements and Release 1 boundaries approved; curriculum and reporting assumptions evidenced with limitations; school workflows validated; data dictionary and database model reviewed; architecture/isolation and offline decision reviewed; privacy/security/threat model reviewed; report catalogue and acceptance/test strategy approved; backup/restore and operational plan tested in a non-production environment; CI and repository controls defined; prioritised implementation backlog approved.

## 11. Open decisions

1. Responsible school governing authority and relevant district/provincial approval route for pilot and data use.
2. Deployment/database isolation model after 1/10/50-school cost and operational comparison.
3. Exact offline scope: release only if all offline acceptance tests pass.
4. Current curriculum, assessment and reporting instruments, and their applicability to the pilot school.
5. Academic calendar, student identifier, transfer and record retention rules.
6. Hosting region, data processing terms, backup retention and operating costs.
7. Approved report template, attendance calculation and achievement descriptors.

**Approval:** Draft only. This charter does not authorise production implementation, live learner-data processing, paid infrastructure or production deployment.
