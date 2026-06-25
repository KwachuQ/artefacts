# Prompt Template: Requirements Generation

**Date:** 2026-06-25
**Author:** Lukasz — Engineering
**Project:** Kepler Insurance (Case B)
**Model:** Claude Opus 4.6
**DIAL location:** N/A — personal tools
**Committed location:** `artefacts/kata2_020/prompt-template-requirements.md`

---

## Purpose

Take rough, unstructured notes about a project or feature and produce a structured requirements document. For any team member starting discovery on a new initiative.

---

## Variable Placeholders

| Placeholder | Description | Example value |
|---|---|---|
| `{{feature_name}}` | Short slug for the feature or project | `kepler-cloud-migration` |
| `{{rough_notes}}` | Raw, unstructured notes about what needs to be built | *"Kepler = insurance group, 50 critical apps need to move..."* |
| `{{stakeholders}}` | Key people or roles involved | CIO, CFO, Claims Ops, Compliance, Migration Lead |
| `{{specific_constraints}}` | Must-not-break rules and hard deadlines | Zero downtime 08-18, 99.95% SLA, SOX audit trail |
| `{{priority_focus}}` | Optional: what to emphasise (risks, compliance, timeline, etc.) | Risks and compliance gaps |

---

## Output Format Instruction

Write to `docs/{{feature_name}}/requirements.md`. Use this structure exactly:

```markdown
# Requirements

## Overview
2-3 sentences. What this is and why it exists.

## Problem Statement
What breaks today without this? Who feels the pain?

## Users
Who uses this. Primary and secondary users if applicable.

## Functional Requirements
- FR-01: [atomic, testable, unambiguous requirement]
- FR-02: [atomic, testable, unambiguous requirement]
...

## Non-Functional Requirements
- NFR-01: [requirement covering performance, reliability, security, observability, or developer experience]
- NFR-02: [requirement]
...

## Out of Scope
Explicitly list what this does NOT do. Be specific.

## Success Metrics
Measurable criteria only. How do we know this is working?

## Assumptions
- [ASSUMED] description of something assumed true but not stated in notes.

## Open Questions
- [TBD] description — why this needs a decision.
```

Rules:
- Never leave a section blank. If unknown, mark `[ASSUMED]` or `[TBD]` with a reason.
- Do not invent requirements not implied by the notes.
- Functional requirements must be traceable — if you can't point to the source, flag as `[ASSUMED]`.
- Be specific: "respond within 5 seconds" not "should be fast".
- Each requirement must be atomic (one thing only), testable (pass/fail), and unambiguous (no "should", "may", "gracefully").
- When done, print a one-line summary: how many FRs, NFRs, assumptions, and open questions were produced.

---

## Prompt Body

You are a technical product manager. Your job is to read rough notes and produce a clean, unambiguous requirements document that will serve as the source of truth for all subsequent architecture and planning work.

**Before writing anything**, identify gaps in the notes and ask the user clarifying questions. Group your questions — don't ask one at a time. Ask everything you need in a single message, then wait for answers before producing the document.

Good questions to consider:
- Who are the users and what does success look like for them?
- Are there performance, reliability or scale requirements not mentioned?
- Are there any implicit technical constraints (language, platform, existing systems)?
- What external services or APIs does this depend on? (AI models, databases, third-party APIs — be specific about providers and versions)
- Where will this run? (local, cloud provider, containerized, serverless)
- What's the MVP vs nice-to-have?
- Are there security, auth or data privacy concerns?

Once you have answers, produce the output file following the Output Format Instruction above.

Feature name: `{{feature_name}}`
Rough notes: {{rough_notes}}
Key stakeholders: {{stakeholders}}
Hard constraints: {{specific_constraints}}
Priority focus: {{priority_focus}}

---

## Test Run (Author)

**Input values used:**
- `{{feature_name}}` = `kepler-cloud-migration`
- `{{rough_notes}}` = *"Kepler = insurance group, 50 critical apps need to move from AWS + some on-prem into Azure, hard stop in 18 months..."* (full notes from notes_source_Kepler.txt)
- `{{stakeholders}}` = CIO, CFO, Claims Ops, Compliance, Migration Lead, Application Owners
- `{{specific_constraints}}` = Zero downtime for claims during business hours, 99.95% SLA on Policy Admin + Claims, SOX audit trail, GDPR/HIPAA/LGPD/APPI compliance
- `{{priority_focus}}` = Risks and compliance gaps

**Output quality:** Usable as-is. The clarifying questions surfaced 7 open questions with owners assigned, and all sections were populated with traceable content. One revision would be to make requirements more atomic (split combined requirements in the risk register into individual items).

---

## Peer Review

**Reviewer:** [To be completed — pair step]
**Date reviewed:** YYYY-MM-DD
**Model used by reviewer:** [Model name]

**Reviewer input values used:**
- `{{placeholder_1}}` = [value reviewer used]
- `{{placeholder_2}}` = [value reviewer used]

| Review question | Reviewer answer |
|---|---|
| Could you run the template without asking the author anything? | Yes / No — [one sentence] |
| Was the output format what you expected? | Yes / No — [one sentence] |
| Would you use this template on your own work? | Yes / No — [one sentence] |
| One concrete improvement suggestion | [One sentence] |

---

## Revision History

| Version | Date | Change | Author |
|---|---|---|---|
| 1.0 | 2026-06-25 | Initial commit | Lukasz |
| 1.1 | | | |