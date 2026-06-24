# Model Selection Note

**Date:** 2026-06-24
**Author:** Lukasz — Engineering
**Project:** Kepler Insurance (Case B)
**Task:** Transform rough notes into a structured requirements document
**Committed location:**  "<https://github.com/KwachuQ/artefacts>"

---

## Evaluation Criteria

| # | Criterion | Why it matters for this task |
|---|-----------|------------------------------|
| 1 | Format compliance | Keeps output predictable; prevents scope creep in the document structure |
| 2 | Completeness | Every key section must be covered for the doc to be actionable |
| 3 | Clarity | Requirements must be atomic, testable, and unambiguous |
| 4 | Assumptions & open questions | Surface unknowns explicitly rather than burying them |

---

## Prompt Used

"Transform the rough notes below into a structured requirements document. Follow this format:

- Project Overview (goal, scope, key stakeholders)
- Constraints & Success Criteria
- Current State / Pain Points
- Risks & Open Questions
- Key Deliverables

For each requirement, make it atomic, testable, and unambiguous.

Notes:

Kepler = insurance group, 50 critical apps need to move from AWS + some on-prem into Azure, hard stop in 18 months because AWS contract expires and can’t be renewed.

Program already 6 months in; only 8/50 apps migrated, mostly easy Tier 3 stuff, so 42 still left and recent Tier 2 waves had post-go-live incidents.

Constraints are nasty: zero downtime for claims during business hours, 99.95 SLA on Policy Admin + Claims, SOX audit trail needed, plus GDPR / HIPAA / LGPD / APPI across regions.

Delivery looks shaky: completed waves are ~40% over budget on average, 6 of 8 migrations had incidents, mostly from missing monitoring/alerting in Azure.

Big messy risk area is ownership/discovery, 11 apps lost original owners, some have no docs, app-owner questionnaire response rate only 60%, and one weird app hits 7 SMTP servers including one in Russia."

---

## Output Comparison

### Model A: Claude Opus 4.6
| Goal | Migrate all 50 critical applications from AWS (and selected on-prem hosts) to Azure before the AWS contract expires. | 

| Hard Deadline | 18 months from program start → ≈ 12 months remaining (6 months already elapsed). | 

| Scope | 42 remaining applications (8 of 50 completed to date, all Tier 3). Remaining backlog includes Tier 2 and Tier 1 workloads. | 

| PP-02 | Persistent post-go-live incidents — 6 out of 8 completed migrations experienced incidents. | Incident reports; root cause predominantly traced to missing monitoring/alerting in Azure. | 

### Model B: DeepSeek V4 Pro
Migrate 50 business-critical applications currently hosted on AWS and on-premises infrastructure to Microsoft Azure within 18 months, driven by a non-renewable AWS contract expiration.

| Apps migrated | 8 of 50 (16%) | Severely behind linear pace (should be ~17 apps) | 

| Average budget variance (completed waves) | +40% over approved budget | Unsustainable burn rate | 

| P-001 | Missing monitoring & alerting in Azure: 6 of 8 completed migrations experienced post-go-live incidents, with root cause traced to absent or misconfigured monitoring/alerting in the target environment. | Increased downtime risk, eroded business confidence, reactive instead of proactive operations. | 

---

## Scorecard

| Criterion | Opus score | Evidence | DeepSeek score | Evidence |
|-----------|-----------|----------|--------------|----------|
| Format compliance | 3 | Strictly followed the 5 requested sections, no extra sections | 2 | Added a 6th "Immediate Actions" section — useful but outside spec |
| Completeness | 3 | All 5 sections present with solid detail | 3 | All sections present with extra detail |
| Clarity | 2 | Requirements slightly more narrative, less atomic | 3 | Each requirement had clear IDs and testable acceptance criteria |
| Assumptions & open questions | 3 | 7 open questions with assigned owners | 2 | Questions present but more generic |
| **Total** | **11** | | **10** | |

---

## Decision

**Selected model:** Claude Opus 4.6

Format compliance is more important as additional content tend to creep in and increase with time. Clarity can be achieved by follow-up questions and giving more context. DeepSeek V4 Pro made more assumptions, which can lead to drift from actual source of truth.
