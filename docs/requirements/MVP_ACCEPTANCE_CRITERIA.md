# Release 1 MVP — Acceptance Criteria

**Document:** ACC-001 | **Version:** 0.2 | **Status:** Draft; requirements and field validation pending

A feature is accepted only when its linked GitHub Issue acceptance criteria pass and evidence is recorded.

## Functional acceptance

- [ ] An authorised administrator can configure the school profile and academic year/periods.
- [ ] Administrator can configure Grades 3–8, class groups/streams, subjects and teacher assignments as validated.
- [ ] Mixed-grade class groups can contain learners from different grades without losing each learner's grade enrolment.
- [ ] Applicable curriculum/standards are selected by each learner's grade and subject, not inferred from class label.
- [ ] Authorised user can create, search and update a student record using approved minimum fields.
- [ ] Student can be enrolled and placed in a class for a defined academic period.
- [ ] Transfer/withdrawal preserves historical enrolment and academic records.
- [ ] Teacher can record attendance for an assigned class/date/session.
- [ ] Duplicate attendance entries are prevented.
- [ ] Corrections are permission-controlled and audited.
- [ ] Authorised teacher can configure an assessment using a supported method and enter criteria/evidence/judgements.
- [ ] Numeric marks are optional and only used where an approved scheme defines them.
- [ ] Missing, pending, not assessed and zero are distinguishable.
- [ ] Historical results remain associated with their original learner, class, subject, curriculum version and period.
- [ ] Individual report cards generate for a selected student and reporting period using an approved template version.
- [ ] Reports show incomplete/unavailable data explicitly.
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
