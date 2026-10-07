---
name: project-charter
description: "Create or revise a software/business Project Charter. Use when a project needs a concise baseline for purpose, objectives, scope, stakeholders, governance, risks, milestones, assumptions, and success criteria before requirements are decomposed into a BRD."
---

# Project Charter

Create a decision-ready Project Charter that establishes why the project exists, who owns it, what is in and out of scope, and how success will be judged.

## Core Principles

- Never invent business facts, owners, dates, budgets, targets, policies, or commitments.
- Treat missing material information as a clarification need, not an invitation to guess.
- Distinguish clearly between **Confirmed**, **Assumption**, **Open Question**, and **Recommendation**.
- Keep the charter strategic. Do not prematurely turn it into a BRD, process specification, user story backlog, or technical design.
- Prefer the user's terminology over generic industry vocabulary.
- Preserve traceability so downstream BRD work can cite charter objectives and scope.

## Upstream Inputs

A Project Charter may be created from:

- project idea or problem statement,
- stakeholder discussion,
- proposal or kickoff notes,
- existing project documentation,
- current-state pain points.

If source documents exist, read them before drafting. When sources conflict, surface the conflict and ask which source controls.

## Interview Gate

Before drafting, assess whether the following are sufficiently known:

1. project/business problem,
2. desired outcome,
3. project sponsor or business owner,
4. project manager or accountable lead,
5. high-level scope,
6. major exclusions,
7. success criteria,
8. major constraints or dependencies,
9. major stakeholders,
10. target timeline or milestone expectations, if they exist.

Ask only questions whose answers materially change the charter. Group related questions. Do not ask for information already available in sources or conversation.

If the user explicitly wants a draft despite gaps, produce it with visible `TBD` or Open Questions rather than fabricating values.

## Workflow

### 1. Understand the project context

Summarize the problem, motivation, desired outcome, stakeholders, and known constraints.

### 2. Separate facts from uncertainty

Maintain an internal classification:

- Confirmed fact
- Assumption requiring validation
- Open question
- Recommendation

Only confirmed facts should be written as definitive project commitments.

### 3. Establish scope boundary

Define:

- In Scope
- Out of Scope
- Deferred / Future Consideration, when useful

Avoid vague boundaries such as “all required features”.

### 4. Define governance

Capture ownership and decision structure at a high level:

- Sponsor / Business Owner
- Product Owner, if applicable
- Project Manager
- Core delivery roles
- Decision authority

Do not invent named people.

### 5. Define measurable success

Prefer measurable or verifiable success criteria. If targets are unknown, describe the desired observable outcome and mark the target as TBD.

### 6. Run a consistency check

Verify that:

- objectives address the stated problem,
- scope supports the objectives,
- success criteria measure the objectives,
- stakeholders match the governance model,
- risks and constraints do not contradict scope or timeline,
- no detailed requirement appears without business context.

## Required Output Structure

Produce Markdown using this default structure, adapting only when the project context demands it:

```markdown
# Project Charter – [Project Name]

## 1. Document Information
## 2. Executive Summary
## 3. Background / Problem Statement
## 4. Project Objectives
## 5. Scope
### In Scope
### Out of Scope
### Deferred / Future Consideration
## 6. Deliverables
## 7. Stakeholders & Governance
## 8. High-Level Timeline / Milestones
## 9. Success Criteria
## 10. Assumptions
## 11. Constraints & Dependencies
## 12. Key Risks
## 13. Open Questions / Decision Log Candidates
## 14. Approval / Baseline
```

Omit empty sections only when they truly do not apply. Prefer `TBD` over invented content.

## Traceability Contract

Assign stable identifiers where useful:

- `OBJ-001` for objectives
- `SCOPE-001` for major scope items
- `SC-001` for success criteria
- `RISK-001` for risks
- `OQ-001` for open questions

The downstream BRD should reference relevant objectives and scope boundaries.

## Quality Gate

Do not finalize until all of the following are true:

- no invented facts,
- objective and scope are distinguishable,
- in-scope and out-of-scope boundaries are explicit,
- governance ownership is understandable,
- success criteria are testable or explicitly TBD,
- open questions are visible,
- document is concise enough to remain a charter rather than a requirements specification.

## Handoff

When the charter is stable, recommend creating a BRD for each major business domain or process that requires detailed requirements.
