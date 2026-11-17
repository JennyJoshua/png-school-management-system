# AI-Assisted Continuous Delivery Workflow

**Document:** DEV-001 | **Version:** 0.2 | **Status:** Proposed operating procedure

## 1. Objective

Deliver PNG-SMS in small, verifiable batches with maximum practical automation while preserving owner approval gates and protecting learner, staff and school information.

## 2. Source of truth

- GitHub Issues: requirements, tasks, defects, decisions and handovers.
- Repository documentation: approved baselines and operating procedures.
- Pull requests: change summary, linked issues, test evidence and review.
- GitHub Actions: repeatable automated validation.

## 3. Delivery cycle

1. Inspect repository, branch, files, workflows, issues and implementation.
2. Confirm issue scope, dependencies, acceptance criteria and exclusions.
3. Plan one small coherent batch.
4. Implement on a feature branch.
5. Validate with relevant automated and manual checks.
6. Review diff, security/privacy, migrations and traceability.
7. Open PR with issue links, tests, risks and deployment/migration impact.
8. Obtain owner approval for gated actions.
9. Merge/deploy only when authorised.
10. Verify outcomes; CI green alone is not release proof.
11. Report completed batch, evidence, outstanding risks and next work.

## 4. Approval controls

Explicit owner approval is required for main merges where the project gate applies, production deployments, hosted database migrations, destructive actions, paid services/upgrades and material scope/architecture changes. Routine non-destructive work within approved scope may proceed.

## 5. Stop conditions

Stop affected work when required tools/data-analysis capability are unavailable for a dependent task; CI blocks; requirements conflict; critical decisions are missing; security/privacy exposure is found; scope exceeds approval; or migration/recovery cannot be validated. Do not claim unverified success.

## 6. Quality and security

- Automated tests for new behaviour.
- Versioned/reviewed migrations; synthetic data only in development and CI.
- Secrets never enter source control.
- School isolation, permissions, audit, export and backup/restore have dedicated tests.
- Shared-device, power-loss and intermittent-connectivity scenarios are considered.
- Offline is not claimed until end-to-end tests pass; otherwise Release 1 is online-only.
- No production learner data in development or CI.

## 7. Data and document safety

Never commit or send to external AI services identifiable learner/staff names, IDs, contact details, signatures, completed registers/report cards, staff rosters, school letterheads, identifiable photos or unredacted scans/screenshots. Blank forms must also be checked for identifying details and permission. Prefer typed field descriptions and synthetic examples. Redaction must be irreversible, not a removable overlay.

## 8. Documentation and reporting

Update requirements, architecture, data dictionary, API, security, user guidance and release notes when decisions change. Avoid repetitive progress narration; report after completed batches.

## 9. Batch report template

- Batch and linked issues
- Delivered
- Tests/checks and evidence
- PR/commit and merge state
- Deployment/verification state
- Risks/deferred items
- Recommended next batch

## 10. Pilot gate

Product-owner approval does not substitute for school-authority approval or data permissions. Identify the responsible school governing authority and relevant district/provincial approval route before real-data use. No real learner data until access, notice/consent where required, retention, security, incident response and operational readiness are documented and approved.
