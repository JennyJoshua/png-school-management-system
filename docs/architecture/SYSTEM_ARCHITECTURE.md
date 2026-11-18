# System Architecture — Proposed MVP

**Document:** ARC-001 | **Version:** 0.3 | **Status:** Proposed; not approved

## 1. Design goals

Independent school data boundaries, one reusable codebase, safe learner-data handling, mobile/low-bandwidth usability, recoverability and future interoperability without dependency on an unknown national platform.

## 2. Logical architecture

Teacher/admin → mobile-first PWA → authenticated API/domain services → enrolment, attendance, curriculum/assessment and reporting modules → school data store → audit and backup/restore. Future versioned integration/export adapter is outside MVP.

## 3. School isolation decision

The topology is unresolved. Options analysis is in [ADR-001](DEPLOYMENT_ISOLATION_DECISION.md). Dedicated app/database per school remains a hypothesis, not a decision. The analysis compares dedicated stacks, shared app with separate databases, shared database with tenant isolation, and a hybrid control/data plane.

No option may proceed unless it passes cross-school isolation, school-level restore/export, incident containment and whole-life cost/supportability criteria. The 1/10/50-school worksheet is not yet populated with verified provider prices; do not treat a free tier as production suitability. P0-06 remains open.

## 4. Technology options

PWA, API/backend, PostgreSQL/Auth, hosting and GitHub Actions remain candidates. Validate region, data processing terms, service availability/sleep limits, backup/restore, access control, secrets, support and total cost. No paid upgrade without explicit approval. No production provisioning is authorised by this proposal.

## 5. Mixed-grade data model implications

A class group may contain learners enrolled in different grades. Keep class group membership, learner's grade-level enrolment, curriculum version, subject assignment and applicable standards distinct. Never infer the learner's curriculum grade from a mixed-grade class label.

## 6. Offline architecture and release gate

Release 1 default is online-only with a validated paper fallback. Offline attendance/assessment is not approved or implemented. [OFF-001](../offline/OFFLINE_SYNC_SPECIFICATION.md) defines local data minimisation, session/device binding, operation IDs, idempotent retry, version checks, conflict handling, sync states, cache expiry, lost-device limits and 18 critical test scenarios. All critical tests and school approval must pass before offline can be enabled. No silent last-write-wins for academic records.

## 7. National integration readiness

Stable identifiers, versioned API, provenance, field definitions, code-list mappings and controlled export/import. No automatic national disclosure or speculative national identifier.

## 8. Environments and decisions

Separate development/test and production. No production learner data in development. Record ADRs for isolation, technology, identity/access, offline, reports/PDF, backup/region and integration. Architecture is not implementation-ready until security, cost and operational decisions are reviewed.

## 9. Decision status

This architecture and linked documents are design artefacts only. They do not authorise application code, physical schema, hosted database, migration, paid service or deployment. P0-06 to P0-08 remain open pending verified evidence and approval.
