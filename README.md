# PNG School Management System (PNG-SMS)

A reusable, modular school-management product for Papua New Guinea primary schools. Release 1 is a focused MVP for student enrolment, class organisation, attendance, assessment records and report-card generation.

## Product direction

- The initial target is PNG primary education (Grades 3–8); elementary Prep–Grade 2 is outside this first primary-school MVP unless separately approved.
- Each participating school has its own application deployment and logically/operationally isolated central database.
- A shared, reusable codebase and common data standards keep deployments maintainable.
- The product must accommodate different school sizes and approved operating practices.
- The data model and APIs must be integration-ready for a future authorised national school-management platform, without depending on that platform for the MVP.
- Staff, assets, equipment and advanced analytics are later releases, not MVP scope.
- Assessment must support standards-based evidence and reporting, not only numeric test marks.

## Proposed technology (not yet locked)

- Mobile-first Progressive Web App (PWA).
- Supabase/PostgreSQL for database and authentication.
- Render for application hosting.
- GitHub for source control, Issues, automated checks and delivery.

Technology choices remain subject to Phase 0 validation, cost/security review and an approved technical baseline. No paid upgrade or production migration is authorised by this document.

## Release roadmap

1. **Release 1 — MVP:** school setup, users/roles, Grades 3–8 configuration, classes, student enrolment, attendance, standards-based assessment records/results, report cards, essential reports, exports and tested backup/recovery.
2. **Release 2:** staff and staff administration.
3. **Release 3:** equipment, inventory and assets.
4. **Release 4:** advanced school reporting and analytics.
5. **Release 5:** national interoperability and authorised data exchange.

## Start here

- [Project Charter](docs/project-charter/PROJECT_CHARTER.md)
- [Product Requirements](docs/requirements/PRODUCT_REQUIREMENTS.md)
- [System Architecture](docs/architecture/SYSTEM_ARCHITECTURE.md)
- [Database Design](docs/database/DATABASE_DESIGN.md)
- [Reporting Requirements](docs/reporting/REPORTING_REQUIREMENTS.md)
- [PNG Curriculum and Assessment Research](docs/research/PNG_CURRICULUM_ASSESSMENT_RESEARCH.md)
- [Security Specification](docs/security/SECURITY_SPECIFICATION.md)
- [MVP Acceptance Criteria](docs/requirements/MVP_ACCEPTANCE_CRITERIA.md)
- [AI-Assisted Continuous Delivery Workflow](docs/delivery/AI_ACD_WORKFLOW.md)
- [Release Roadmap](docs/release-notes/RELEASE_ROADMAP.md)
- [Phase 0 Backlog](docs/requirements/PHASE_0_BACKLOG.md)

## Project status

**Phase:** 0 — discovery and foundation.  
**Baseline status:** Draft for owner review. Requirements, curriculum/reporting rules, architecture and database design must be validated and approved before implementation. No production application or database is implied to exist.

## Working principles

Small delivery batches; GitHub Issues as the work register; evidence-based testing; documented decisions; privacy by design; offline reliability; no unapproved paid services, destructive actions, production deployments, merges or hosted database migrations.
