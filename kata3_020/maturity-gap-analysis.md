# Maturity Gap Analysis

**Date:** 2026-06-25
**Author:** Lukasz — Engineering
**Project:** Python Mentoring Program / AI RUN 2026
**Committed location:** `artefacts/kata3_020/maturity-gap-analysis.md`

---

## Scorecard

| Dimension | Level (L1 / L2 / L3) | Score (1.0 / 2.0 / 3.0) | Evidence (2–3 sentences) |
|---|---|---|---|
| AI Capabilities | L1 | 1.0 | I use AI tools daily — a Python Coding Tutor Perplexity space, AI Mentor Beta on learn.epam.com, and reusable skills for my final project. However, usage is entirely personal and self-directed; there is no shared practice, no standardised tools, and nobody else in the cohort coordinates AI use with me. One colleague agreed to peer-review katas, but that is an informal arrangement, not a team practice. |
| Reusability | L1 | 1.0 | I have created reusable assets: a requirements prompt template (Kata 2 output) and a curated Perplexity space for Python theory. However, these live in my personal toolchain only — there is no shared repository, no team norm around saving prompts, and no one else in the cohort references or contributes to shared assets. |
| AI Champions | L1 | 1.0 | There is no named person driving AI adoption at cohort level. I have one colleague who agreed to peer-review katas, but neither of us champions adoption beyond our own work. The Python Mentoring Program has no designated AI Champion role. |
| Performance Tracking | L1 | 1.0 | I use SonarQube to assess code quality and track complexity scores of AI-generated code. However, this is personal quality checking — there are no shared metrics, no team-wide productivity tracking, and no structured measurement of AI's impact on delivery speed or quality across the cohort. |
| DAU | L1 | 1.0 | I use AI daily myself, but I have no data on how many others in the Python Mentoring cohort do. I estimate daily AI use among the cohort at below 30% — based on the fact that no shared practices, tools, or adoption discussions exist. This is an estimate, not a measured figure. |
| **Average** | | **1.0** | |
| **Overall Level** | | | L1 (1.0–1.9) |

---

## Gap Analysis

### Gap 1

**Dimension:** Reusability
**Current level:** L1
**Why this gap is most damaging:** Without a shared repository and team norm for reusable assets, personal templates stay personal — the shift from individual efficiency to compound team leverage never happens.
**Root cause:** There is no designated location for shared prompts or skills, and no team norm that requires committing reusable assets to a shared location.

---

### Gap 2

**Dimension:** Performance Tracking
**Current level:** L1
**Why this gap is most damaging:** Without structured metrics, there is no way to evaluate whether changes to the AI workflow are improving quality or speed — which blocks optimisation of the agentic SDLC loop, a core goal of this course.
**Root cause:** No habit or tooling exists for logging AI output quality metrics over time — current assessment is ad-hoc and limited to spot checks in SonarQube.

---

## 30-Day Improvement Plan

### Step 1 — addresses Gap 1 (Reusability)

| Field | Value |
|---|---|
| **Action** | Create a `katas/` folder in the artefacts repo and migrate all 3 Module 020 kata outputs there. Share the folder path with the peer reviewer colleague and invite them to commit their own outputs. |
| **Owner** | Lukasz |
| **Timeline** | 2026-07-09 |
| **Success metric** | At least 1 kata artifact from the colleague committed to the shared folder |

---

### Step 2 — addresses Gap 2 (Performance Tracking)

| Field | Value |
|---|---|
| **Action** | Define 2 simple metrics — SonarQube complexity score and time spent per kata — and log them in a tracking file for the next 30 days. |
| **Owner** | Lukasz |
| **Timeline** | 2026-07-25 |
| **Success metric** | At least 10 tracked entries in the log with before/after comparison data |

---

## Peer Review

**Reviewer:** [To be completed — pair step]
**Date reviewed:** YYYY-MM-DD

| Review question | Reviewer answer |
|---|---|
| Is the evidence for each dimension specific and observable — not aspirational? | [One sentence] |
| Which score do you challenge, and why? | [At least one — dimension, proposed alternative score, reason] |
| Is each root cause a structural/behavioural cause — not a symptom? | Yes / No — [one sentence] |