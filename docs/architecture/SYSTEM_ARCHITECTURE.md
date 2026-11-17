# System Architecture — Proposed MVP

**Document:** ARC-001 | **Version:** 0.2 | **Status:** Proposed; not approved

## 1. Design goals

Independent school data boundaries, one reusable codebase, safe learner-data handling, mobile/low-bandwidth usability, recoverability and future interoperability without dependency on an unknown national platform.

## 2. Logical architecture

Teacher/admin → mobile-first PWA → authenticated API/domain services → enrolment, attendance, curriculum/assessment and reporting modules → school data store → audit and backup/restore. Future versioned integration/export adapter is outside MVP.

## 3. School isolation decision

Separate app deployment and database per school is the leading hypothesis, not a decision. Compare at least:
- Separate deployment + database per school.
- Shared application with isolated per-school database/schema and enforceable identity boundary.
- Any other viable model supported by evidence.

For each option, estimate full operating cost and operational effort at 1, 10 and 50 schools: hosting, database, backups, monitoring, upgrades, support, incident response, restore and data export. Evaluate isolation strength, failure blast radius, backup granularity, recovery, maintenance burden and portability. Define pass/fail thresholds before selecting. A free tier alone is not a pass. If no model meets security and sustainability thresholds, pause expansion and revisit the business/operating model rather than weaken controls.

## 4. Technology options

PWA, API/backend, PostgreSQL/Auth, hosting and GitHub Actions remain candidates. Validate region, data processing terms, service availability/sleep limits, backup/restore, access control, secrets, support and total cost. No paid upgrade without explicit approval.

## 5. Mixed-grade data model implications

A class group may contain learners enrolled in different grades. Keep class group membership, learner's grade-level enrolment, curriculum version, subject assignment and applicable standards distinct. Never infer the learner's curriculum grade from a mixed-grade class label.

## 6. Offline architecture and release gate

Offline capture is optional for Release 1 unless end-to-end tests pass. Specify minimum local data, protected storage, device/session binding, operation IDs, idempotent retry, conflict detection/resolution, sync status, cache expiry/clearing, lost-device response, shared-device handover and recovery. No silent last-write-wins for conflicting academic records. If any critical test fails or remains unimplemented, release online-only and defer offline.

## 7. National integration readiness

Stable identifiers, versioned API, provenance, field definitions, code-list mappings and controlled export/import. No automatic national disclosure or speculative national identifier.

## 8. Environments and decisions

Separate development/test and production. No production learner data in development. Record ADRs for isolation, technology, identity/access, offline, reports/PDF, backup/region and integration. Architecture is not implementation-ready until security, cost and operational decisions are reviewed.
