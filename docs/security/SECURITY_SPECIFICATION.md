# Security and Privacy Specification — MVP

**Document:** SEC-001 | **Version:** 0.2 | **Status:** Draft for review

## 1. Security objectives

Protect learner, guardian, staff and school operational information; prevent cross-school access; preserve academic record integrity; ensure only authorised users can view or change records.

## 2. Data protection principles

- Collect only necessary information for a defined school purpose.
- Document purpose, access, retention, correction and authorised disclosure.
- Use synthetic/de-identified data in development and CI.
- Real learner data requires documented authority, appropriate notice/consent where required, approved access and pilot safeguards.
- Never commit learner or staff names, identifiers, contact details, signatures, handwritten annotations, identifiable photos, completed registers/report cards, staff rosters, school letterheads or scanned official records to a public repository.
- Blank forms may still contain identifying letterheads, signatures or contact details; obtain permission and redact before sharing.
- Screenshots must be inspected and irreversibly redacted before any repository or external-service use. Prefer written field descriptions over screenshots.
- Do not send identifiable learner/staff data to external AI services or unrelated third parties.
- Verify applicable PNG privacy, child protection, education-record and retention obligations with competent advice; do not claim compliance without evidence.

## 3. Authentication and access

Individual accounts only; no shared accounts. Least-privilege role-based access, school boundary enforced server-side and at database boundary, class/subject assignment constraints, prompt revocation and audited role changes. Shared-device sign-out and session expiry must be tested.

## 4. Application and data security

HTTPS; protected secrets; no privileged database key in client; validation/encoding; parameterised queries; rate limits; safe errors; secure upload controls if files are introduced; minimise personal data in logs/analytics.

## 5. Audit and integrity

Audit authentication, access changes, enrolment, placements, attendance, assessments, report generation, exports, configuration and security events. Capture actor, timestamp, action, record reference and reason where relevant. Ordinary users cannot alter audit records.

## 6. Backups, recovery and incident response

Define encryption, frequency, retention, access, restore testing, recovery objectives, incident reporting, containment, credential rotation and notification decision. A backup is not accepted until restore is demonstrated.

## 7. Offline device controls

Minimise local cache; protect it; bind to authorised user/device/session; clear on logout/expiry; support revocation and lost-device response. Shared-device handover must not expose prior user's records. Offline release requires tested conflict and recovery behaviour.

## 8. School isolation

Separate credentials and backups where separate deployments are used. Test cross-school access through API, database policies, exports and guessed identifiers. Cross-school disclosure is release-blocking.

## 9. Release security gates

Threat model; dependency/security review; permission and isolation tests; secret scan; transport verification; restore test; incident procedure; shared-device tests; offline tests if offline is included. Critical/high unresolved findings block pilot.

## 10. Legal and policy validation

Obtain appropriate advice on applicable PNG legal and education obligations. This is a technical starting point, not legal advice or a compliance certification.
