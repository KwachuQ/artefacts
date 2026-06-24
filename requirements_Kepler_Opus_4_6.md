# Kepler Insurance — Cloud Migration Requirements

> **Source**: [notes_source_Kepler.txt](file:///c:/Users/lkwas/Desktop/AI_RUN_2026/artefacts/notes_source_Kepler.txt)
> **Date**: 2026-06-24

---

## 1 · Project Overview

| Field | Detail |
|---|---|
| **Client** | Kepler Insurance Group |
| **Goal** | Migrate all 50 critical applications from AWS (and selected on-prem hosts) to Azure before the AWS contract expires. |
| **Hard Deadline** | 18 months from program start → **≈ 12 months remaining** (6 months already elapsed). |
| **Scope** | 42 remaining applications (8 of 50 completed to date, all Tier 3). Remaining backlog includes Tier 2 and Tier 1 workloads. |
| **Key Stakeholders** | Kepler IT leadership, application owners (where identifiable), compliance / audit team, claims operations, infrastructure & cloud engineering. |

---

## 2 · Constraints & Success Criteria

### 2.1 Non-Negotiable Constraints

| ID | Constraint | Verification |
|---|---|---|
| **C-01** | AWS contract cannot be renewed; all workloads must be fully decommissioned from AWS within 12 remaining months. | AWS billing shows zero active resources by deadline. |
| **C-02** | Zero downtime for Claims processing during defined business hours (hours TBD per region). | Synthetic-transaction monitoring confirms no service interruption during each migration window. |
| **C-03** | Policy Admin and Claims systems must meet a **99.95 % SLA** post-migration. | Azure Monitor / SLA reports show ≥ 99.95 % monthly uptime for 3 consecutive months post-cutover. |
| **C-04** | Full **SOX audit trail** must be maintained throughout and after migration. | Audit team sign-off that change-control records, access logs, and data-lineage artifacts satisfy SOX requirements. |
| **C-05** | All migrated workloads must comply with **GDPR, HIPAA, LGPD, and APPI** as applicable by region. | Compliance assessment per application confirms data-residency, consent, and breach-notification obligations are met in Azure. |

### 2.2 Success Criteria

| ID | Criterion | Measure |
|---|---|---|
| **SC-01** | All 50 applications running in Azure with AWS fully decommissioned. | Infrastructure inventory reconciliation. |
| **SC-02** | Post-go-live incident rate per wave ≤ 1 (P1/P2). | Incident log comparison against current baseline (6 incidents in 8 migrations = 75 %). |
| **SC-03** | Migration wave budget variance ≤ +10 % of estimate. | Actuals vs. estimates per wave (current baseline: +40 %). |
| **SC-04** | Monitoring and alerting operational in Azure **before** each cutover. | Pre-cutover readiness checklist sign-off including dashboard and alert validation. |

---

## 3 · Current State / Pain Points

| ID | Pain Point | Evidence |
|---|---|---|
| **PP-01** | Low migration velocity — 8 of 50 apps in 6 months, all Tier 3 (easiest). | Program tracker. |
| **PP-02** | Persistent post-go-live incidents — 6 out of 8 completed migrations experienced incidents. | Incident reports; root cause predominantly traced to missing monitoring/alerting in Azure. |
| **PP-03** | Significant budget overruns — completed waves average ~40 % over budget. | Finance actuals vs. estimates. |
| **PP-04** | 11 applications have lost their original owners; documentation is absent or stale. | App-owner questionnaire non-responses. |
| **PP-05** | App-owner questionnaire response rate is only 60 %, leaving 40 % of discovery data incomplete. | Questionnaire tracker. |
| **PP-06** | At least one application has undocumented external dependencies — contacts 7 SMTP servers, including one located in Russia (potential compliance / data-sovereignty issue). | Network traffic analysis. |

---

## 4 · Risks & Open Questions

### 4.1 Risks

| ID | Risk | Impact | Suggested Mitigation |
|---|---|---|---|
| **R-01** | Remaining 12 months insufficient to migrate 42 apps at current velocity (~1.3 apps/month). | Miss AWS contract deadline; emergency renewal or outage. | Re-plan wave schedule; parallelize waves; add capacity; prioritize Tier 1 apps. |
| **R-02** | Tier 1 / Tier 2 apps are more complex than Tier 3; incident rate may increase. | Extended outages on business-critical systems. | Mandatory pre-cutover readiness gates (monitoring, rollback, load testing). |
| **R-03** | Orphaned apps (11) cannot be safely migrated without owner sign-off and dependency mapping. | Data loss, broken integrations, compliance gaps. | Assign interim owners; run automated dependency discovery tooling. |
| **R-04** | SMTP dependency on a Russian server may violate GDPR / data-sovereignty rules. | Regulatory fine, audit finding. | Immediate investigation: identify what data flows, obtain legal opinion, reroute or decommission. |
| **R-05** | Continued budget overruns erode program funding before all 42 apps are migrated. | Program stalls or gets cancelled. | Root-cause the +40 % variance; introduce estimation review gates; re-baseline remaining waves. |

### 4.2 Open Questions

| ID | Question | Owner |
|---|---|---|
| **OQ-01** | What are the defined "business hours" per region for the zero-downtime Claims constraint (C-02)? | Claims Operations |
| **OQ-02** | Is the Tier classification (1/2/3) documented and agreed? What criteria define each tier? | Program Office |
| **OQ-03** | Can the AWS contract deadline be extended under any emergency clause, or is it truly immovable? | Procurement / Legal |
| **OQ-04** | Which of the 42 remaining apps carry HIPAA, LGPD, or APPI obligations (vs. GDPR only)? | Compliance |
| **OQ-05** | What monitoring / alerting stack is targeted in Azure (Azure Monitor, Datadog, etc.) and is there a standard to enforce before cutover? | Cloud Engineering |
| **OQ-06** | For the 11 orphaned apps, is there a fallback decision authority who can approve migration without original owner sign-off? | Program Sponsor |
| **OQ-07** | What is the purpose and data classification of the traffic to the Russian SMTP server? | Security / Compliance |

---

## 5 · Key Deliverables

| ID | Deliverable | Description |
|---|---|---|
| **D-01** | **Revised Wave Plan** | Updated schedule covering all 42 remaining apps, grouped by tier and dependency, fitting within the 12-month window. |
| **D-02** | **Application Discovery & Dependency Map** | Complete inventory for every app: owner (or assigned interim owner), architecture, integrations, data flows, compliance tags. |
| **D-03** | **Pre-Cutover Readiness Checklist** | Gate criteria each wave must pass before go-live, including monitoring, alerting, rollback plan, load-test results, and compliance sign-off. |
| **D-04** | **Monitoring & Alerting Baseline** | Standard Azure monitoring configuration deployed and validated for every application before cutover (addresses root cause of PP-02). |
| **D-05** | **Compliance Evidence Pack** | Per-application documentation proving SOX, GDPR, HIPAA, LGPD, and APPI compliance post-migration. |
| **D-06** | **Budget Re-Baseline** | Revised cost estimates for remaining waves incorporating lessons learned from the +40 % overrun pattern. |
| **D-07** | **Russian SMTP Investigation Report** | Findings on the app contacting 7 SMTP servers (including Russia), with remediation recommendation and legal sign-off. |
