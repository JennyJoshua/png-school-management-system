# Release 1 MVP — Acceptance Criteria

**Document:** ACC-001 | **Version:** 0.1 | **Status:** Draft

A feature is accepted only when its linked GitHub Issue acceptance criteria pass and evidence is recorded.

## Functional acceptance

- [ ] An authorised administrator can configure the school profile and academic year/periods.
- [ ] Administrator can configure grades, classes/streams, subjects and teacher assignments.
- [ ] Authorised user can create, search and update a student record.
- [ ] Student can be enrolled and placed in a class for a defined academic period.
- [ ] Transfer/withdrawal preserves historical enrolment and academic records.
- [ ] Teacher can record attendance for an assigned class/date/session.
- [ ] Duplicate attendance entries are prevented.
- [ ] Corrections are permission-controlled and audited.
- [ ] Authorised teacher can configure an assessment and enter valid student results.
- [ ] Invalid scores and duplicate results are rejected with clear messages.
- [ ] Historical results remain associated with their original class, subject and period.
- [ ] Individual report cards generate for a selected student and reporting period.
- [ ] Missing results are distinguishable from zero.
- [ ] Attendance summaries use an approved, documented calculation.
- [ ] Reports preview, print and download as PDF without clipped content.
- [ ] Class lists, attendance and assessment summaries are available.
- [ ] Authorised exports validate and preserve identifiers and relationships.

## Security and operational acceptance

- [ ] Each user has an individual account.
- [ ] Role and class/subject permissions are enforced server-side.
- [ ] Cross-school access tests fail safely.
- [ ] No privileged secrets are exposed in browser bundles or repository.
- [ ] Important changes and access administration are audited.
- [ ] Backup is configured and a restoration test succeeds.
- [ ] Deployment and rollback/recovery steps are documented.
- [ ] Real learner data is not used before pilot safeguards and authority are approved.

## Offline acceptance (only if included in the release)

- [ ] Assigned register data is available offline within the approved cache scope.
- [ ] Attendance/assessment entries can be queued offline.
- [ ] Sync retries are idempotent.
- [ ] Pending, synced and failed states are visible.
- [ ] Conflicts are detected and resolved without silent overwrite.
- [ ] Lost-device/session-revocation behaviour is tested.
- [ ] Supported Android browser and intermittent-connectivity tests pass.

## Quality acceptance

- [ ] Automated unit, integration and end-to-end tests pass.
- [ ] CI checks pass on the release candidate.
- [ ] No unresolved critical/high security defects.
- [ ] Accessibility and mobile usability checks pass.
- [ ] Performance is tested against agreed school-sized data and network conditions.
- [ ] User acceptance testing is completed by authorised pilot representatives.
- [ ] Release notes, user guidance and support/recovery procedures are available.

## Release decision

Release requires documented evidence, closure or explicit acceptance of known defects, owner approval at required gates, and successful pilot readiness review. Passing CI alone does not prove the product is ready.
