# AI-Assisted Continuous Delivery Workflow

**Document:** DEV-001 | **Version:** 0.1 | **Status:** Proposed operating procedure for this repository

## 1. Objective

Deliver PNG-SMS in small, verifiable batches with maximum practical automation while preserving owner approval gates and protecting learner data.

## 2. Source of truth

- GitHub Issues: requirements, implementation tasks, defects, decisions and handovers.
- Repository documentation: approved product/technical baselines and operating procedures.
- Pull requests: implementation summary, linked issues, test evidence and review discussion.
- GitHub Actions: repeatable automated validation.

## 3. Delivery cycle

1. **Inspect:** inspect repository, current branch, files, workflows, issues and existing implementation before changing anything.
2. **Specify:** confirm the issue has scope, dependencies, acceptance criteria and out-of-scope notes.
3. **Plan batch:** choose a small coherent set of issues; avoid mixing unrelated changes.
4. **Implement:** make changes on a feature branch; keep commits understandable.
5. **Validate:** run relevant formatting, lint, type, unit, integration, security and end-to-end checks.
6. **Review:** inspect the diff, security/privacy implications, migrations and requirement traceability; correct failures.
7. **Pull request:** link issues, describe changes, list tests/results, migration and deployment impact, and known limitations.
8. **Approval gate:** obtain owner approval where required before main merges, production deployments, paid services/upgrades, destructive actions, material scope changes and hosted database migrations.
9. **Merge/deploy:** merge only under the approved gate; deploy only when authorised.
10. **Verify:** confirm the deployed version and critical user journeys; do not infer success from a green build alone.
11. **Report:** provide a concise batch report: completed issues, changed areas, tests and evidence, merge/deployment state, outstanding risks and next batch.

## 4. Approval controls

Explicit owner approval is required for:
- Main-branch merges when the project gate applies.
- Production deployment.
- Hosted database migrations or schema changes affecting live data.
- Destructive actions or irreversible data changes.
- Paid services, upgrades or material operating-cost commitments.
- Material scope/architecture changes.

Routine coding, local testing, documentation and non-destructive review within an approved issue may proceed without repeated approval.

## 5. Stop conditions

Stop the affected work and report when:
- Required tools or data-analysis capability are unavailable where the task depends on them.
- CI has a blocking failure.
- Requirements conflict or a critical decision is missing.
- A security/privacy defect or possible data exposure is found.
- A change exceeds approved scope or approval is required.
- A migration cannot be safely validated or recovered.

Do not claim tests, merges, deployments or fixes that have not been confirmed.

## 6. Quality and security gates

- Automated tests are required for new behaviour.
- Database migrations are versioned, reviewed and tested against representative data.
- No production learner data in development/CI.
- Secrets never enter source control.
- School isolation, permissions, audit and backup/recovery receive dedicated tests.
- CI success is necessary but not sufficient for release.
- Failed checks must be investigated and corrected before advancing the affected batch.

## 7. Documentation

Update requirements, architecture decisions, database dictionary, API contracts, user guidance and release notes when implementation changes them. Avoid repetitive process narration; report after completed batches.

## 8. Batch report template

- Batch and linked Issues:
- Delivered:
- Tests/checks and results:
- PR/commit:
- Merge status:
- Deployment/verification status:
- Risks or deferred items:
- Recommended next batch:

## 9. Data safety

Use synthetic data for development. Real learner data requires explicit pilot readiness, school authority, approved access, privacy safeguards and secure operational controls. Never copy student records into issue descriptions or public logs.
