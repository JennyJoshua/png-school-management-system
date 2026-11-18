# Privacy and Security Threat Model

**Document:** THR-001  
**Version:** 0.1  
**Status:** Draft — validation required  
**Related issue:** [P0-07](https://github.com/JennyJoshua/png-school-management-system/issues/7)  
**Companion:** SEC-001 Security and Privacy Specification

## 1. Scope and assumptions

This model covers a future multi-school system holding learner, guardian, staff, enrolment, attendance, assessment, report, school and account data. It is a design-time model, not evidence that controls have been implemented or tested.

Assumptions to validate:
- Learners are children and their records require heightened protection.
- Staff may use shared or personally owned phones, including devices with limited storage and intermittent connectivity.
- Schools may have variable connectivity, power and local technical support.
- School administrators, teachers and support operators have different legitimate access needs.
- A school may leave the service and require an export and controlled offboarding.

## 2. Assets and data classes

| Asset | Examples | Proposed sensitivity | Primary protection |
|---|---|---|---|
| Learner identity | Name, date of birth, school ID, guardian link | Restricted | Minimal collection, role scope, encryption, audit |
| Learner academic record | Grade placement, attendance, assessment evidence, report card | Restricted | Record-level authorization, integrity, correction history |
| Guardian contact | Phone, email, relationship | Restricted | Purpose limitation, access restriction |
| Staff identity | Name, contact, role, employment/assignment details | Confidential / restricted | Least privilege, retention and disclosure controls |
| Credentials and sessions | Password hashes, tokens, recovery secrets | Critical | Secure authentication, hashing, rotation, short-lived sessions |
| School configuration | School profile, class, term, subject settings | Internal | School boundary, admin authorization, audit |
| Files and evidence | Work samples, photos, uploaded documents | Restricted | Private storage, upload validation, access expiry |
| Audit and operational logs | Actor, time, event, record reference | Confidential | Minimise payloads, restricted access, tamper resistance |
| Backups and exports | Database snapshots, CSV/PDF bundles | Restricted | Encryption, access control, retention, restore/export audit |
| Local offline cache | Queued attendance or assessment changes | Restricted | Device/session binding, encryption where feasible, expiry, revocation |

Do not collect sensitive personal data unless a specific approved school purpose and lawful basis are established. Avoid storing identity documents or unnecessary medical/family details in Release 1.

## 3. Threat register

Likelihood and impact are preliminary qualitative ratings (Low / Medium / High), not measured probabilities. Residual risk remains open until implementation tests pass.

| ID | Threat / failure | Likelihood | Impact | Required mitigation | Verification test | Accountable role |
|---|---|---|---|---|---|---|
| T-01 | Account takeover through weak/reused password or recovery abuse | Medium | High | Secure password policy, rate limits, secure recovery, session revocation, MFA for privileged roles where feasible | Automated auth abuse and recovery tests | Security/operator |
| T-02 | Shared phone exposes prior user's session or cached records | High | High | Individual accounts, explicit sign-out, short inactivity expiry, cache clearing, no shared credentials | Handover test across two users and revoked account | School admin + operator |
| T-03 | Teacher accesses learners outside assigned class/subject | Medium | High | Server-side class/subject scope and deny-by-default authorization | Attempt direct API access to unassigned learner | Product/security |
| T-04 | Cross-school data leakage through tenant routing, query, report, export or guessed ID | Medium | Critical | Strong school boundary, separate credentials/data stores where selected, database enforcement, tenant-aware tests | Two-school adversarial API/DB/export suite | Operator |
| T-05 | Privileged operator or school admin misuses access | Medium | High | Least privilege, time-bound support access, approval and audit, break-glass procedure | Review role matrix and privileged action audit | System owner |
| T-06 | Incorrect or malicious academic record alteration | Medium | High | Validation, actor/time audit, correction workflow, versioning, no ordinary hard delete | Concurrent edit, correction and audit integrity tests | Academic admin |
| T-07 | Export or printed report left on shared device/printer | High | High | Explicit export permission, purpose confirmation, expiry, no public links, user guidance, audit | Export permission and shared-printer scenario | School admin |
| T-08 | Sensitive data exposed in logs, analytics, error reports or support tickets | Medium | High | Structured redacted logs, no request-body logging for sensitive endpoints, access and retention limits | Seed canary values and scan logs | Operator |
| T-09 | Backup theft, misconfiguration or failed restore | Medium | Critical | Encryption, isolated backup credentials, retention, restore drills, alerting | Restore from isolated backup and access review | Operator |
| T-10 | Malicious or unsafe uploaded file | Medium | High | Restrict file types/size, private storage, generated object names, malware scanning where available, safe download headers | Upload abuse and access tests | Product/security |
| T-11 | Lost/stolen device contains offline records or queued writes | High if offline enabled | High | Minimise cache, device/session binding, expiry, remote revocation, recovery workflow | Lost-device and revocation simulation | Operator |
| T-12 | Offline duplicate, conflict or stale write corrupts attendance/assessment | Medium if offline enabled | High | Operation IDs, idempotency, version checks, explicit conflict queue, no silent last-write-wins | Duplicate/reorder/concurrent update tests | Product/QA |
| T-13 | Third-party AI, analytics, email or hosting provider receives excessive data | Medium | High | Data minimisation, provider due diligence, no identifiable data to AI by default, contracts and transfer review | Data-flow review and outbound payload inspection | System owner |
| T-14 | Public repository or screenshot exposes names, signatures, letterheads or records | Medium | High | Synthetic data only, scan/redaction review, access controls, secret scanning | Repository and artifact review | Maintainer |
| T-15 | School offboarding leaves active accounts, data copies or public exports | Medium | High | Revocation checklist, export validation, retention/deletion decision, backup lifecycle | Full school exit drill | Operator + school authority |
| T-16 | Denial of service, provider outage or power/network interruption blocks school work | High | Medium–High | Graceful failure, documented paper fallback, backups, status/incident communication; offline only if proven | Outage and paper fallback exercise | Operator + school admin |
| T-17 | Dependency, secret or deployment compromise | Medium | High | Dependency updates/scanning, secret management, protected deployment workflow, least-privilege CI | CI security checks and credential rotation drill | Maintainer/operator |
| T-18 | Legal/policy obligations misunderstood or retention excessive | Medium | High | Competent PNG legal/education/privacy advice, approved retention schedule and notice | Documented authority/legal review | System owner + competent authority |

## 4. Proposed role/permission matrix

This is a starting policy; exact school titles and delegation require validation. All permissions are scoped to one school and, where applicable, assigned class/subject.

| Capability | System operator | School head / delegated admin | Teacher | Read-only auditor |
|---|---:|---:|---:|---:|
| Provision school tenant | Yes, controlled | No | No | No |
| Manage school profile/settings | Support-only, audited | Yes | No | Read |
| Invite/disable school users | No routine use; emergency only | Yes | No | Read |
| Assign class/subject | No routine use | Yes | No | Read |
| View learner identity | Support access only by approved exception | School scope | Assigned scope | Approved scope |
| Manage enrolment/placement | No routine use | Yes | Limited request/entry if delegated | Read |
| Record attendance | No | Yes if delegated | Assigned class | Read |
| Create assessment/results | No | Oversight/correction approval | Assigned class/subject | Read |
| Correct locked/published results | No | Controlled approval with reason | Request only | Read |
| Generate/export reports | No routine use | School scope | Assigned scope, limited | Approved scope |
| View audit events | Platform security events | School events | Own relevant events only | Approved scope |
| Delete/purge records | Restricted operational process only | No ordinary hard delete | No | No |

**Rules:** deny by default; server-side checks on every request; client-hidden buttons are not security; privileged access must be logged; no cross-school browsing by default; corrections preserve history.

## 5. Privacy lifecycle questions

Before real data:
- What is the documented purpose for each field, who is the responsible data controller/authority, and who may authorise processing?
- What notice is given to guardians and staff? Is consent required, and where is another lawful basis applicable?
- What is the minimum retention period for enrolment, attendance, assessment, reports, audit and backups?
- How can a school/guardian request correction, and who approves it?
- What happens when a learner transfers, leaves school or reaches the end of retention?
- Which records must be retained for statutory/education purposes and for how long?
- Where are primary data, backups, logs and support copies hosted and processed?
- What incident notification obligations and timeframes apply?
- What contracts and subprocessor disclosures are needed?

These are unresolved questions. This document is not legal advice and does not certify compliance with PNG law or Department of Education requirements.

## 6. Incident response minimum

1. Detect and record the suspected event without copying sensitive payloads into tickets.
2. Contain: revoke sessions/credentials, disable affected integration or export, isolate affected tenant/service as appropriate.
3. Preserve minimal evidence with restricted access and timestamps.
4. Assess affected schools, data classes, records, exposure window and likely harm.
5. Notify the responsible school authority and obtain competent advice on any required notifications.
6. Recover from a known-good state; verify integrity and cross-school isolation.
7. Rotate credentials, patch root cause and document lessons.
8. Close only after the responsible authority accepts the remediation evidence.

## 7. Pilot-blocking conditions

Any unresolved Critical or High risk without an approved and tested mitigation blocks real learner-data pilot use. A policy statement alone is not a control. Offline mode remains disabled unless the separate offline release gate passes.

## 8. Evidence still required

- Confirmed school roles and delegated authority.
- PNG legal, child-protection, education-record and privacy validation.
- Selected hosting/data-flow topology and provider terms.
- Implemented permission matrix and automated isolation tests.
- Restore, incident, export and offboarding drill evidence.
- Approved retention schedule and privacy notices.
