# Kepler Cloud Migration Program — Requirements Document

**Document Version:** 1.0  
**Date:** 2026-06-24  
**Classification:** Confidential  

---

## 1. Project Overview

### 1.1 Goal
Migrate 50 business-critical applications currently hosted on AWS and on-premises infrastructure to Microsoft Azure within 18 months, driven by a non-renewable AWS contract expiration.

### 1.2 Scope

| Dimension | In Scope | Out of Scope |
|---|---|---|
| **Applications** | 50 critical apps (Tier 1, Tier 2, Tier 3) | Non-critical / deprecated apps |
| **Source Environments** | AWS (primary), on-premises data centers | Third-party SaaS platforms |
| **Target Environment** | Microsoft Azure (IaaS + PaaS) | Multi-cloud or hybrid ongoing operation |
| **Regions** | All regions where Kepler operates | New region expansion |
| **Compliance** | SOX, GDPR, HIPAA, LGPD, APPI | Future regulatory frameworks not yet enacted |

### 1.3 Key Stakeholders

| Role | Responsibility |
|---|---|
| **Program Sponsor (C-level)** | Funding, escalation, strategic alignment |
| **Program Manager** | Overall delivery, timeline, budget governance |
| **Application Owners (per app)** | App-specific discovery, testing, sign-off |
| **Cloud Architecture Team** | Target-state design, Azure landing zones |
| **Security & Compliance Officer** | SOX audit trail, data residency, regulatory sign-off |
| **Infrastructure / DevOps** | CI/CD pipelines, monitoring, alerting, IaC |
| **Business Unit Leads** | UAT coordination, business-hours continuity |
| **External SI Partner (if any)** | Migration execution, wave planning |

---

## 2. Constraints & Success Criteria

### 2.1 Hard Constraints (Non-Negotiable)

| ID | Constraint | Rationale / Source |
|---|---|---|
| **C-001** | All 50 applications MUST be fully migrated to Azure and decommissioned from AWS within 18 calendar months of program start (i.e., by the AWS contract expiry date). | AWS contract is non-renewable; running past expiry incurs penalty rates or service termination. |
| **C-002** | Claims-processing systems MUST experience zero downtime during business hours (Mon–Fri, 08:00–18:00 local time per region) throughout the migration. | Regulatory and customer-impact requirement. |
| **C-003** | Policy Administration and Claims systems MUST maintain 99.95% availability SLA (measured monthly, inclusive of planned migration windows). | Contractual obligation to brokers and policyholders. |
| **C-004** | All migration activities and configuration changes MUST produce a complete, immutable SOX-compliant audit trail. | Sarbanes-Oxley Act, Section 404. |
| **C-005** | Data residency and processing MUST comply with GDPR (EU), HIPAA (US health data), LGPD (Brazil), and APPI (Japan) for all in-scope applications handling personal data in those jurisdictions. | Multi-region regulatory exposure. |

### 2.2 Success Criteria (Measurable)

| ID | Criterion | Measurement Method | Target |
|---|---|---|---|
| **S-001** | All 50 applications running in Azure with AWS dependencies fully severed. | Inventory audit, AWS billing cessation | 50/50 by deadline |
| **S-002** | Zero Severity-1 incidents attributable to migration within 30 days post-go-live per wave. | Incident management system | 0 Sev-1 per wave |
| **S-003** | Each migration wave completed within ±10% of approved budget. | Financial tracking vs. wave budget | ≤10% variance |
| **S-004** | 100% of applications have monitoring and alerting configured in Azure before go-live. | Azure Monitor / Sentinel dashboard audit | 100% pre-go-live |
| **S-005** | 100% of application-owner questionnaires completed and signed off before wave start. | Document management system | 100% per wave |
| **S-006** | All compliance controls (SOX, GDPR, HIPAA, LGPD, APPI) verified by independent audit within 60 days of final migration. | External audit report | Zero critical findings |

---

## 3. Current State / Pain Points

### 3.1 Program Status (as of Month 6)

| Metric | Value | Assessment |
|---|---|---|
| **Elapsed time** | 6 of 18 months (33%) | — |
| **Apps migrated** | 8 of 50 (16%) | Severely behind linear pace (should be ~17 apps) |
| **Apps remaining** | 42 | — |
| **Tier distribution of completed** | Mostly Tier 3 (low complexity) | Hardest work still ahead |
| **Average budget variance (completed waves)** | +40% over approved budget | Unsustainable burn rate |
| **Waves with post-go-live incidents** | 6 of 8 (75%) | Indicates systemic quality issues |

### 3.2 Pain Points

| ID | Pain Point | Impact |
|---|---|---|
| **P-001** | **Missing monitoring & alerting in Azure:** 6 of 8 completed migrations experienced post-go-live incidents, with root cause traced to absent or misconfigured monitoring/alerting in the target environment. | Increased downtime risk, eroded business confidence, reactive instead of proactive operations. |
| **P-002** | **Budget overruns:** Completed waves averaging ~40% over budget. At current trajectory, the remaining 42 apps will exhaust the program budget before completion. | Program may require additional funding or face scope reduction. |
| **P-003** | **Application ownership gaps:** 11 of 50 applications have no identified current owner (original owners have left or roles changed). | Blocks discovery, delays decision-making, increases risk of missed dependencies. |
| **P-004** | **Incomplete documentation:** Several applications lack architecture diagrams, dependency maps, runbooks, or configuration records. | Extends discovery phase, increases likelihood of missed integrations during cutover. |
| **P-005** | **Low questionnaire response rate:** Only 60% of app-owner questionnaires have been completed and returned. | Discovery is incomplete; migration plans for 40% of apps are based on assumptions, not verified data. |
| **P-006** | **Anomalous application behavior:** One application connects to 7 distinct SMTP servers, including one hosted in Russia. | Potential security, compliance, and data-exfiltration risk. Requires immediate investigation before migration. |

---

## 4. Risks & Open Questions

### 4.1 Risk Register

| ID | Risk Description | Likelihood | Impact | Mitigation |
|---|---|---|---|---|
| **R-001** | **Schedule slippage:** At current velocity (8 apps / 6 months), the remaining 42 apps will take ~32 months — far exceeding the 12 months remaining. | High | Critical | Re-plan waves for parallelism; increase automation; augment team capacity; escalate Tier 1/2 apps immediately. |
| **R-002** | **Budget exhaustion:** If the +40% overrun trend continues, the program will require 40% more funding than approved. | High | High | Implement stricter wave budget controls; root-cause the overruns; establish a contingency reserve. |
| **R-003** | **Business disruption from incidents:** 75% incident rate on remaining 42 apps could cause significant claims-processing outages. | High | Critical | Mandate monitoring/alerting as a go-live gate; introduce pre-prod performance/soak testing; implement automated rollback plans. |
| **R-004** | **Compliance violation:** Incomplete discovery (especially the SMTP/Russia anomaly) may hide data-residency or data-sovereignty violations. | Medium | Critical | Immediate security review of the anomalous app; engage DPO for Russia data-flow assessment; mandate data-flow mapping for all Tier 1 apps. |
| **R-005** | **Ownerless applications stall waves:** 11 apps without owners cannot complete discovery, testing, or sign-off. | High | High | Escalate to business unit heads to assign interim owners within 2 weeks; treat as blocking dependency for wave scheduling. |
| **R-006** | **SOX audit failure:** Incomplete or non-immutable audit trails during migration could result in a qualified audit opinion. | Medium | High | Design and implement SOX-compliant change-tracking in Azure before next wave; validate with internal audit. |
| **R-007** | **Key-person dependency:** Low questionnaire response may indicate over-reliance on a small number of individuals who could become bottlenecks or leave. | Medium | Medium | Identify single points of knowledge; enforce cross-training; tie questionnaire completion to wave entry criteria. |

### 4.2 Open Questions

| ID | Question | Owner | Target Answer Date |
|---|---|---|---|
| **Q-001** | What is the exact AWS contract expiry date, and what are the financial penalties for overrun? | Program Sponsor / Legal | Within 1 week |
| **Q-002** | Who will serve as interim application owners for the 11 ownerless apps? | Business Unit Heads | Within 2 weeks |
| **Q-003** | What is the nature of the application connecting to 7 SMTP servers, and is the Russia-based server authorized? | Security / DPO | Within 1 week |
| **Q-004** | What is the current remaining program budget, and has a contingency reserve been allocated? | Program Manager / Finance | Within 1 week |
| **Q-005** | Are there existing Azure landing zones, or do they need to be built in parallel with migration? | Cloud Architecture Team | Within 2 weeks |
| **Q-006** | What is the Tier classification criteria (Tier 1, 2, 3), and what is the full inventory with tier assignments? | Program Manager | Within 1 week |
| **Q-007** | What automation tooling (Azure Migrate, Terraform, etc.) is already in place, and what gaps exist? | Infrastructure / DevOps | Within 2 weeks |

---

## 5. Key Deliverables

### 5.1 Program-Level Deliverables

| ID | Deliverable | Description | Acceptance Criteria | Due |
|---|---|---|---|---|
| **D-001** | **Re-baselined Migration Plan** | A revised wave plan that achieves 42 app migrations in 12 months, with realistic parallelism, dependencies mapped, and Tier 1/2 apps prioritized. | Plan reviewed and approved by all stakeholders; resource-loaded; critical-path identified. | Month 7 |
| **D-002** | **Azure Landing Zone (if not already built)** | Standardized, compliant Azure foundation including networking, identity, policy, logging, and security controls for all target workloads. | Landing zone passes security and compliance review; all subsequent waves deploy into it. | Month 8 |
| **D-003** | **Monitoring & Alerting Framework** | Standardized Azure Monitor / Application Insights / Sentinel configuration template mandatory for every application before go-live. | Template validated; included as a go-live gate in the migration checklist; 100% adoption across all waves. | Month 7 |
| **D-004** | **SOX Audit Trail Solution** | Immutable logging of all migration activities, configuration changes, and approvals, integrated with Azure Policy and Log Analytics. | Demonstrated to internal audit; audit trail queryable and exportable; retention policy meets SOX requirements. | Month 7 |
| **D-005** | **Compliance Control Matrix** | Per-application mapping of GDPR, HIPAA, LGPD, and APPI controls with verification evidence for each migrated app. | 100% of in-scope apps have completed control matrix; signed off by DPO. | Per wave + final by Month 18 |

### 5.2 Per-Wave Deliverables (Applicable to Each Migration Wave)

| ID | Deliverable | Description | Acceptance Criteria |
|---|---|---|---|
| **D-101** | **Completed App-Owner Questionnaire** | Full discovery questionnaire signed by the application owner covering dependencies, data flows, integrations, performance baselines, and compliance requirements. | 100% complete; no unanswered sections; signed by owner. |
| **D-102** | **Application Dependency Map** | Visual and documented map of all upstream/downstream dependencies, data stores, and external integrations. | Reviewed by architecture team; no unknown dependencies. |
| **D-103** | **Migration Runbook** | Step-by-step cutover plan including pre-migration checks, execution steps, validation tests, and rollback procedure. | Dry-run tested; rollback procedure executed successfully in pre-prod. |
| **D-104** | **Pre-Prod Validation Report** | Results of performance testing, soak testing, security scanning, and compliance checks in the Azure pre-production environment. | All tests pass; performance within 10% of baseline; no critical/high security findings. |
| **D-105** | **Go-Live Checklist (signed)** | Checklist covering: monitoring active, alerts configured, backup verified, DR tested, runbook approved, rollback on standby, business sign-off obtained. | All items checked and signed by app owner, DevOps lead, and business lead. |
| **D-106** | **Post-Go-Live Stability Report (30-day)** | Incident summary, performance metrics, availability SLA attainment, and any open remediation items 30 days after cutover. | Zero Sev-1 migration-attributable incidents; SLA met; remediation items assigned with due dates. |

---

## 6. Immediate Actions (Next 30 Days)

| Priority | Action | Owner |
|---|---|---|
| **P0** | Investigate the application with 7 SMTP servers / Russia connection — security and DPO assessment | Security / DPO |
| **P0** | Assign interim owners for the 11 ownerless applications | Business Unit Heads |
| **P1** | Re-baseline the migration plan for 42 apps in 12 months | Program Manager |
| **P1** | Design and mandate the monitoring/alerting go-live gate | DevOps / Architecture |
| **P1** | Chase outstanding questionnaires; escalate non-response to program sponsor | Program Manager |
| **P2** | Root-cause analysis of +40% budget overruns on completed waves | Program Manager / Finance |
| **P2** | Validate Azure landing zone readiness or initiate build | Cloud Architecture |
| **P2** | Implement SOX-compliant audit trail in Azure | Security / DevOps |

---

*End of Document*