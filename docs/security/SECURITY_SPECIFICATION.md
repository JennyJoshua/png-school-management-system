# Security and Privacy Specification — MVP

**Document:** SEC-001 | **Version:** 0.1 | **Status:** Draft for review

## 1. Security objectives

Protect learner and guardian information, prevent cross-school access, preserve academic record integrity and ensure that only authorised staff can view or change records.

## 2. Data protection principles

- Collect only data required for defined school functions.
- Document purpose, access, retention and authorised disclosure.
- Use synthetic/de-identified data in development and automated tests.
- Obtain appropriate school authority and provide suitable notice/consent before processing real learner data.
- Do not publish student records, report cards or identifiable screenshots.
- Do not send learner data to external AI services or unrelated third parties.
- Define a process for correction, export, retention and secure deletion consistent with applicable PNG law and school policy. Legal requirements must be verified, not assumed.

## 3. Authentication and access

- Individual accounts only; no shared accounts.
- Secure password/session handling and supported account recovery.
- Role-based permissions with least privilege.
- School-scoped access enforced server-side and at the database boundary.
- Class/subject assignment limits teacher access to relevant records.
- Immediate account disable/revocation when access is no longer required.
- Administrator actions and role changes are audited.

## 4. Data and application security

- HTTPS for all network traffic.
- Secrets stored in protected environment variables/secret management, never committed to Git.
- No database service-role key or privileged credential in client code.
- Input validation, output encoding and safe error handling.
- Parameterised database access and dependency updates.
- Rate limiting and abuse protection for authentication/API endpoints.
- Secure file handling if uploads are introduced.
- Avoid exposing unnecessary personal data in logs, analytics or error messages.

## 5. Audit and integrity

Audit authentication/security events and material changes to enrolment, class placement, attendance, assessment results, report generation, exports, user roles and school settings. Record actor, timestamp, action, record reference and reason where applicable. Ordinary users cannot alter audit events.

## 6. Backups and incident response

Document backup frequency, encryption, retention, access, restore testing and recovery objectives. A backup is not accepted until a restoration test succeeds. Define incident reporting, containment, credential rotation, investigation, notification decision and recovery procedures before pilot launch.

## 7. Offline device controls

Minimise locally cached student data. Protect local storage, bind cached data to an authorised session/device, expire or revoke access, provide logout/cache clearing and lost-device procedures. Offline data must not be accessible to the next device user. Test device loss and account revocation scenarios.

## 8. School isolation

Each deployment/database has distinct credentials and backups. Test attempts to access another school's records through API, database policies, exports and guessed identifiers. Any cross-school disclosure is a release-blocking security defect.

## 9. Release security gates

Before pilot: threat model, dependency/security review, role/permission tests, school-isolation tests, backup restoration, secret scan, transport-security verification and documented incident procedure. Critical/high unresolved findings block release.

## 10. Legal and policy validation

Confirm applicable PNG privacy, child protection, education-record and data-retention obligations with appropriate authoritative advice. This document is a technical starting point, not legal advice or a claim of regulatory compliance.
