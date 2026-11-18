# School Deployment and Database Isolation Decision

**Document:** ADR-001  
**Version:** 0.1  
**Status:** Options analysis — decision deferred  
**Related issue:** [P0-06](https://github.com/JennyJoshua/png-school-management-system/issues/6)  
**Depends on:** DD-001 data dictionary; ARC-001 system architecture

## 1. Decision to be made

Choose an operating model that provides enforceable school-to-school confidentiality, manageable recovery and support, and sustainable whole-life cost. A low initial hosting price or a free tier is not sufficient evidence.

**No production topology is approved by this document.** The separate application/database per school approach remains a hypothesis, not a locked decision.

## 2. Options

| Option | Description | Strong points | Main risks / costs |
|---|---|---|---|
| A. Dedicated stack per school | Separate application deployment, database, credentials, storage and backup set for each school | Clear tenant boundary; school-level restore/export; smaller breach blast radius | Repeated upgrades, monitoring, backups, support and configuration; cost grows approximately with school count |
| B. Shared app, separate database per school | One maintained application service routes to separate school databases with strict tenant-to-connection mapping | Strong database boundary with fewer app deployments | Routing/control-plane becomes critical; one routing defect can expose multiple schools; central service availability affects all |
| C. Shared app, shared database with schema/row isolation | Shared application and database; school scope enforced by database roles/policies and server-side authorization | Potentially lower infrastructure and upgrade overhead | Highest consequence if tenant policy, query scoping or privileged credentials are wrong; complex cross-tenant testing and restore |
| D. Hybrid control plane + isolated school data planes | Central catalogue/identity or deployment manager; school data stores remain independently isolated | Can automate provisioning while preserving school-level data boundaries | More moving parts, operational complexity and central control-plane security requirements |

No option is accepted solely because a vendor offers a free tier or because it is easiest to prototype.

## 3. Non-negotiable pass/fail criteria

An option fails if it cannot demonstrate all of the following before real learner data:
1. A school user cannot read, infer, modify, export or delete another school's records through UI, API, database, guessed identifiers, reports, search, background jobs or support tooling.
2. School identity is established server-side from trusted authentication/tenant configuration; client-supplied school IDs are never trusted as the sole control.
3. Least-privilege credentials are separated by environment and, where practical, by school.
4. Backups and restore can be performed for one school without exposing another school's data.
5. School exit includes verified export, retention/deletion decision and credential revocation.
6. Monitoring and logs do not expose unnecessary learner/staff data.
7. A tested incident containment path exists for compromised school credentials and cross-school exposure.
8. Whole-life cost and support workload are sustainable at 1, 10 and 50 schools.

A cross-school disclosure, inability to restore a school independently, or inability to export a school's records is a release-blocking failure.

## 4. 1 / 10 / 50-school operating model

No vendor or hosting topology has been approved, and current provider pricing, regional availability, contractual terms, backup features and free-tier limits have not yet been validated. Therefore numeric totals are intentionally **not fabricated** here.

| Cost / effort driver | 1 school | 10 schools | 50 schools | Evidence required |
|---|---|---|---|---|
| Application hosting | One production service or shared service | One-to-many deployment or shared service | Fleet automation likely required | Current provider price, limits, region, sleep/uptime, bandwidth |
| Database compute/storage | One isolated DB or shared DB | 10 isolated DBs or shared DB capacity | 50 isolated DBs or scaled shared capacity | Compute, storage, connection, backup and egress prices |
| Backup and restore | One backup policy and restore drill | Per-school retention/restore operations | Automated fleet-level verification essential | Included backup scope, PITR, retention, restore charges |
| Monitoring/logging | One service set | Centralised dashboards plus school dimensions | Alert routing and automation required | Event/ingestion limits, retention, sensitive-data controls |
| Upgrades/security patches | One deployment | Coordinated rollout and rollback | Staged automated rollout and fleet inventory | Engineering and release effort |
| Support/onboarding | One school setup and training | Repeated onboarding and support | Repeatable self-service/process likely needed | Staff hours per onboarding, incident and support case |
| Data export/exit | One school export | Repeatable school-specific export | Automated validated exports | Format, completeness, time and storage/egress |
| Incident/recovery | One school incident path | Multiple independent school incidents | Fleet triage and blast-radius controls | RTO/RPO targets and drill results |

### Calculation worksheet

For each option and school count N ∈ {1, 10, 50}, calculate:

- Monthly infrastructure = application + database + storage + backups + monitoring + bandwidth/egress + email/identity + other required services.
- One-time onboarding = provisioning + configuration + data setup + training.
- Monthly operations effort = monitoring + patching + backup verification + support + incident allowance.
- Annual whole-life cost = 12 × monthly infrastructure + annualised onboarding/engineering/support effort.
- Per-school cost = annual whole-life cost ÷ N.

Record provider, pricing page/quote date, currency, assumptions, free-tier expiry/limits, taxes/FX assumptions and excluded items. Separate cash cost from volunteer/owner labour. Test growth and restore workload, not only idle hosting.

## 5. Provisional evaluation

| Criterion | A: dedicated stack | B: app + separate DB | C: shared DB | D: hybrid |
|---|---|---|---|---|
| Tenant isolation clarity | Strong | Strong if routing is correct | Depends heavily on database policy and privileged paths | Strong for data plane |
| Cross-school blast radius | Usually smaller | Routing/control plane can widen it | Potentially broad | Depends on control-plane privileges |
| Per-school restore/export | Direct | Direct with automation | More complex | Direct if data plane isolated |
| Upgrade effort | Highest | Medium | Lowest application fleet effort | Medium–high |
| Operational complexity | Many stacks | Routing + many databases | Policy and query correctness | Highest initial architecture complexity |
| Likely cost at small scale | Potentially higher | Potentially medium | Potentially lower | Potentially higher |
| Evidence status | Unpriced | Unpriced | Unpriced | Unpriced |

These are qualitative hypotheses, not benchmark results or a selection.

## 6. Required tests before decision

- Automated cross-school API and database isolation tests, including guessed IDs and export/report endpoints.
- Privileged service-role and support-access review.
- Independent school backup, restore, export and exit drill.
- Credential rotation and school offboarding drill.
- Failure simulation for app, database, routing/control plane and backup provider.
- Cost worksheet populated from current provider evidence for N=1,10,50.
- Operational runbook and named accountable operator role.

## 7. Provisional recommendation and decision gate

Retain dedicated school data boundaries as the design priority. Do not yet choose between a fully dedicated stack and an automated shared application with separate school databases. Defer shared-database row-level isolation unless it can pass the same independent security and restore tests with compelling measured cost/operations evidence.

P0-06 remains **open** until the price/effort model, provider evidence, thresholds, tests and owner decision are recorded. No service provisioning or paid commitment is authorised.

## 8. Open decisions

- Required availability target and acceptable maintenance window.
- Recovery point objective (RPO) and recovery time objective (RTO).
- Data hosting location and applicable cross-border obligations.
- Who operates support, incident response, backup verification and school exit.
- Whether schools can pay for a dedicated deployment and ongoing support.
- Provider terms, pricing and service limits at the date of decision.
