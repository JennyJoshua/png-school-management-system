# Offline Capture and Synchronisation Specification

**Document:** OFF-001  
**Version:** 0.1  
**Status:** Proposed design — not approved or implemented  
**Related issue:** [P0-08](https://github.com/JennyJoshua/png-school-management-system/issues/8)  
**Dependencies:** DD-001 data dictionary, ADR-001 isolation decision, THR-001 threat model

## 1. Release decision

Offline attendance and assessment capture is **not currently approved for Release 1**. The safe default is online-only operation with a documented paper fallback.

Offline may be enabled only after every critical security, integrity, recovery and usability test in this specification passes on supported devices. If any critical test fails, remains unimplemented or cannot be evidenced, Release 1 remains online-only. Do not imply that a PWA or service worker automatically provides safe offline capability.

## 2. Scope boundary

Potential offline actions, subject to school validation:
- Capture attendance for a previously assigned class and school day.
- Draft assessment observations/evidence and outcomes for learners within the teacher's assigned class/subject.
- Queue changes and synchronise them when connectivity returns.

Not permitted offline in initial scope:
- User/role administration, enrolment transfer or grade/class placement changes.
- Bulk export, report publication, payment or school configuration.
- Changes to curriculum versions, grading rules or published/locked results.
- Access to a full school register or broad search cache.
- Offline access after account revocation, session expiry or school reassignment.

Offline data must be minimised to the minimum assigned roster and task data needed for the active session.

## 3. Local data and device protection

Before enabling offline:
- Use individual accounts; never shared credentials.
- Bind offline capability to authenticated user, school, device installation and expiry window.
- Store only assigned learner identifiers/display names and the minimum task/roster fields.
- Do not cache guardian contacts, full learner profiles, bulk reports, credentials, tokens in plaintext or unrelated classes.
- Prefer platform-protected storage; assess encryption at rest and browser/PWA limitations on every supported device.
- Define cache expiry, logout clearing, session revocation, device replacement and lost-device response.
- Show a clear offline warning and last successful sync time.
- Shared-device handover must clear the prior user's local data before the next user can enter.
- If the platform cannot reliably protect and clear the cache, offline is not eligible.

A browser/PWA running on an unmanaged shared phone may not provide sufficient remote-wipe or hardware-backed protection. This limitation must be included in the release decision.

## 4. Queue record and write protocol

Every offline operation must contain:
- Globally unique operation ID generated once and retained for all retries.
- School ID and actor ID derived from the authenticated session, not trusted from editable client fields.
- Device/session installation reference and schema/version.
- Target record ID, operation type and minimum payload.
- Base record version or last-known server revision.
- Client-created timestamp and local sequence number.
- Explicit status: queued, sending, accepted, conflict, rejected or needs-review.

Server protocol:
1. Authenticate the user and validate active account, school, device/session and assignment at sync time.
2. Validate operation type, payload, schema version, target school and record scope.
3. Enforce unique operation ID per tenant; a repeated ID returns the original result and does not apply the write twice.
4. Compare base version/current state; reject or route stale conflicting writes to review.
5. Commit record change and operation receipt atomically.
6. Return a durable server receipt and current version.
7. Client marks accepted only after receipt; rejected/conflict operations remain visible and recoverable.

Never trust client clock, client-supplied actor, school or role as proof of authority. Never silently overwrite a server value using last-write-wins for attendance or assessment.

## 5. Synchronisation state machine

| State | Meaning | Allowed transition |
|---|---|---|
| Local draft | User is editing, not yet queued | Save locally or discard with confirmation |
| Queued | Immutable operation envelope awaits sync | Sending when network is available |
| Sending | Request in flight | Accepted, conflict, rejected or retryable error |
| Accepted | Server receipt confirms durable commit | Terminal; local queue may be compacted under retention rules |
| Conflict | Server state changed or concurrent operation exists | Human review/resolution, then new operation ID |
| Rejected | Authentication, scope, validation or policy failure | Explain reason; re-authenticate or correct via a new operation |
| Retryable error | Timeout/network/server unavailable | Retry same operation ID with bounded backoff |
| Needs review | Ambiguous result or unrecoverable local state | Preserve evidence and require authorised manual reconciliation |

Do not delete a queued item merely because a request timed out. Query the operation receipt or retry with the same ID. If the server committed but the response was lost, idempotency must return the original result.

## 6. Conflict policy

- Attendance: two edits to the same learner/date/session based on different versions create a conflict. A teacher or authorised school admin reviews both values and the reason; the system records the resolution and actor. No automatic overwrite.
- Assessment evidence: preserve each evidence item as a separate immutable submission where appropriate. Conflicting edits to a shared judgement require review and audit.
- Published/locked records: offline writes cannot modify them. A correction request must be submitted online through the approved correction workflow.
- Assignment or role revoked since the device last synchronised: reject the queued write and retain a safe audit record; do not accept stale authority.
- Learner moved or withdrawn: do not infer authority from an old roster; route to authorised review.
- Duplicate operation ID: return the original receipt without applying again.
- Duplicate human action with different operation IDs: apply domain-specific duplicate detection and require review where ambiguity remains.

## 7. Power, connectivity and device-loss behaviour

- Intermittent network: retain queued operations and show pending count/last sync; retry without duplicate writes.
- Sudden power loss: recover only operations durably saved before power loss; unsaved edits may be lost and must be clearly communicated.
- Browser storage eviction/clear: detect missing local queue and show a recovery warning; never claim queued work was synchronised.
- Lost/stolen device: revoke account/device session; on next connection clear local cache. Acknowledge that remote clearing cannot be guaranteed while device remains offline.
- Shared device: require explicit sign-out, cache clearing and next-user clean-state verification.
- Long offline period: expire the local capability after a configured, validated maximum; require online re-authentication before sync.
- Schema upgrade: do not attempt to sync unsupported queue versions; preserve exportable recovery metadata and require controlled migration/review.

## 8. Test gate

All critical tests must pass on the actual supported low-cost Android devices/browsers and realistic low-connectivity conditions. Use synthetic records only.

| ID | Scenario | Required result |
|---|---|---|
| O-01 | Capture attendance online, then offline | Local draft/queue clearly shown; no false server confirmation |
| O-02 | Network drops during sync after server commit | Retry same operation ID; one server change only |
| O-03 | Duplicate retry / double tap | No duplicate attendance or evidence |
| O-04 | Two devices edit same attendance record | Conflict surfaced; no silent overwrite |
| O-05 | Teacher assignment revoked while device offline | Sync rejected after reconnection |
| O-06 | Account disabled/session revoked | No new offline access after revocation is known; sync rejected |
| O-07 | Shared phone user A signs out, user B signs in | A's cached data/queue inaccessible to B |
| O-08 | Device lost while offline | Document residual exposure; no claim remote wipe is guaranteed |
| O-09 | Power interruption during local save | Only durable operations recover; queue integrity verified |
| O-10 | Browser storage cleared/evicted | Missing queue detected; no silent loss claim |
| O-11 | Long offline period / expired session | Re-authentication required; stale authority not accepted |
| O-12 | Learner transferred or class assignment changed | Stale roster cannot authorise write |
| O-13 | Published result edited offline | Rejected; correction workflow required |
| O-14 | Malformed/tampered school or actor ID | Server ignores client authority fields and rejects invalid scope |
| O-15 | Unsupported queued schema version | Safe hold/recovery; no partial application |
| O-16 | Restore server from backup after accepted sync | Accepted writes and operation receipts consistent |
| O-17 | Multiple queued operations arrive out of order | Domain ordering/version checks preserve integrity |
| O-18 | No power/network for a school day | Paper fallback usable and later reconciliation documented |

Critical failures: cross-school access, unauthorised writes, duplicate application, silent data loss, hidden conflict, prior-user cache exposure, or accepted write without durable receipt.

## 9. Operational fallback

Until offline is approved:
- Teachers use the school's existing authorised paper attendance/assessment record.
- Data entry occurs when a trusted connection is available.
- A designated authorised user reconciles paper records; discrepancies are retained with a reason and date.
- The application must distinguish not entered, absent, present and zero numeric score; missing data is not interpreted as zero.
- The school retains its approved paper records according to its own policy.

Paper fallback itself must be validated with the reference school and should not introduce unnecessary personal-data copying.

## 10. Release gate and decision record

Offline is eligible only when:
- Device/browser support matrix is documented.
- Threat model accepts residual local-device risks.
- Local storage, session binding, expiry and shared-device controls are implemented and tested.
- Idempotency, versioning, conflict and recovery protocol is implemented and tested.
- All critical O-01–O-18 tests pass with retained evidence.
- School authority approves the operational workflow and paper fallback.
- Incident, lost-device and support runbooks are ready.

Until these conditions are met, **Release 1 mode = online-only**. P0-08 remains open; no offline implementation is authorised by this specification.
