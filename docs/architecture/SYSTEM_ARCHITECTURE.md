# System Architecture — Proposed MVP

**Document:** ARC-001 | **Version:** 0.1 | **Status:** Proposed; not approved

## 1. Design goals

1. Independent operation and data isolation for each school.
2. One reusable codebase and repeatable school deployment.
3. Safe handling of learner data.
4. Usable mobile experience under intermittent connectivity.
5. Simple, maintainable MVP with later modular expansion.
6. Future interoperability without coupling to an unknown national platform.

## 2. Logical architecture

```text
Teacher / School Administrator
          |
     Mobile-first PWA
          |
   Authenticated API layer
          |
 Domain modules / services
   |        |        |
Students Attendance Assessments
   |        |        |
 Reporting / PDF / Export
          |
 School-specific PostgreSQL database
          |
 Backup / restore / audit

Future: versioned integration API and export/import adapter
        to an authorised national platform (not in MVP)
```

## 3. School deployment model

Preferred starting model: deploy the same application version separately for each school, with a separate school database and independent credentials, backup and configuration. This provides a strong operational boundary and avoids relying solely on application-level tenant filters.

Validate the cost and maintenance burden before locking this model. Alternative isolation models may be assessed, but no design may permit one school's users to query another school's data.

Each deployment has:
- immutable deployment/school identity;
- its own database credentials and secrets;
- school-specific configuration and logo;
- independent backup and restore procedure;
- versioned schema migrations;
- controlled export for school-authorised transfer.

The codebase must not contain school-specific business logic forks.

## 4. Proposed technology options

- Frontend: mobile-first PWA; framework selection during Phase 0.
- Backend: secure API and domain layer; framework selection during Phase 0.
- Database/authentication: Supabase-managed PostgreSQL and Auth are proposed.
- Hosting: Render is proposed for application services.
- Source control/CI: GitHub and GitHub Actions.

These are proposals, not an approved commitment. Validate free-tier limits, sleep/availability behaviour, backup capabilities, regional availability, data processing terms, security controls and expected operating costs. No paid upgrades without owner approval.

## 5. Core modules

MVP modules: school configuration, identity/access, academic structure, student/enrolment, class placement, attendance, assessment/results, reporting/export and audit.

Later modules must be separately bounded: staff; assets/equipment; advanced analytics; national interoperability.

## 6. Offline architecture

Offline mode is a high-risk feature and must be specified before implementation:
- cache only the minimum authorised class/student data needed;
- use protected local storage and device/session controls;
- queue mutations with unique operation IDs;
- make sync retries idempotent;
- show pending/synced/failed status;
- detect concurrent edits and require resolution where automatic merge is unsafe;
- log sync outcomes;
- provide a lost-device/session-revocation procedure.

Never silently use last-write-wins for conflicting attendance or assessment records. Define retention and local-cache deletion behaviour. Offline capability is not accepted until tested on supported Android browsers and real intermittent-connectivity scenarios.

## 7. National integration readiness

Prepare stable internal identifiers, versioned API contracts, documented field definitions, code-list mapping, export/import formats and provenance fields. Keep national identifiers optional until official standards are confirmed. No automatic national transfer or disclosure in MVP.

## 8. Environments and deployment

Use separate development/test and production environments. Never use production learner data in development. Database changes use reviewed, version-controlled migrations with backup and rollback/recovery plans. Production migration and deployment require explicit approval.

## 9. Architecture decisions to record

Create Architecture Decision Records (ADRs) for:
- per-school database/deployment isolation;
- frontend/backend framework;
- authentication and role model;
- offline local storage and sync/conflict strategy;
- PDF/report generation;
- backup/restore and hosting region;
- national identifier and integration mapping.

## 10. Quality attributes and validation

Security, privacy, data isolation, offline reliability, performance, accessibility, backup recovery and export portability require explicit tests. The architecture is not implementation-ready until these are reviewed and approved.
