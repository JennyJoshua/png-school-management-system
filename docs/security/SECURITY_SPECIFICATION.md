# Security and Privacy Specification — MVP

**Document:** SEC-001 | **Version:** 0.3 | **Status:** Draft for review

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

Individual accounts only; no shared accounts. Least-privilege role-based access, school boundary enforced server-side and at database boundary, class/subject assignment constraints, prompt revocation and audited role changes. Shared-device sign-out and session expiry must be tested. The proposed role/capability matrix and threat register are in [THR-001](THREAT_MODEL.md); school roles and delegated authority still require validation.

## 4. Application and data security

HTTPS; protected secrets; no privileged database key in client; validation/encoding; parameterised queries; rate limits; safe errors; secure upload controls if files are introduced; minimise personal data in logs/analytics.

## 5. Audit and integrity

Audit authentication, access changes, enrolment, placements, attendance, assessments, report generation, exports, configuration and security events. Capture actor, timestamp, action, record reference and reason where relevant. Ordinary users cannot alter audit records. Corrections preserve history rather than silently rewriting published academic outcomes.

## 6. Backups, recovery and incident response

Define encryption, frequency, retention, access, restore testing, recovery objectives, incident reporting, containment, credential rotation and notification decision. A backup is not accepted until restore is demonstrated. School-specific restore/export and incident containment must be proven for the selected deployment topology.

## 7. Offline device controls

Offline is not approved for Release 1. If reconsidered, minimise local cache; protect it; bind to authorised user/device/session; clear on logout/expiry; support revocation and lost-device response. Shared-device handover must not expose prior user's records. [OFF-001](../offline/OFFLINE_SYNC_SPECIFICATION.md) defines the protocol and test gate. The inability to guarantee remote clearing of a lost device while it is offline is an explicit residual risk.

## 8. School isolation

The selected isolation model is pending P0-06. Enforce school boundaries server-side and at the data layer. Test cross-school access through API, database policies, exports, reports, background jobs and guessed identifiers. Cross-school disclosure is release-blocking. See [ADR-001](../architecture/DEPLOYMENT_ISOLATION_DECISION.md).

## 9. Release security gates

Threat model; dependency/security review; permission and isolation tests; secret scan; transport verification; restore test; incident procedure; shared-device tests; offline tests if offline is included. Critical/high unresolved findings block pilot. [THR-001](THREAT_MODEL.md) lists preliminary threats and verification requirements; risk ratings are qualitative and require review.

## 10. Legal and policy validation

Obtain appropriate advice on applicable PNG legal and education obligations. This is a technical starting point, not legal advice or a compliance certification. Retention periods, notices, lawful basis, cross-border processing and notification obligations remain unresolved.

## 11. Status and limits

This specification is a draft, not a security certification or evidence of implemented controls. No real learner/staff data, production deployment or hosted database is authorised by this document.
