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

## Interactive Interview Protocol

When clarification is required, **prefer the agent harness's native interactive user-input/question tool instead of asking a plain-text questionnaire in chat**.

### Input control selection

Choose the control that matches the decision:

- **Single-select / options**: use when the user must choose one of several known, mutually exclusive business alternatives.
- **Multi-select / checkboxes**: use when several known alternatives may apply at the same time.
- **Free-text / text field**: use when the answer is a factual value that cannot be safely inferred, such as a role name, business rule, threshold, reason, document name, or process description.
- **Options + Other/free-text**, when supported: use when common choices are known but the user may have a different business-specific answer.

### Interview behavior

- If the harness exposes a structured question tool, use it. Do not replace it with a manually formatted Markdown list of questions.
- Group only closely related questions in one interaction. Prefer **1–3 high-value questions** per round so the user can answer accurately.
- Reuse facts already known from the conversation or upstream documents. Never ask the same question twice.
- For business facts, do **not** provide a “You decide” option. The agent must not choose facts on the user's behalf.
- Options must be neutral and materially distinct. Do not steer the user toward the agent's recommendation.
- When one option is recommended, label the recommendation separately from the answer choices or explain it after the user answers.
- Use free-text fields for unknown facts rather than inventing placeholder values.
- If an answer introduces a new ambiguity, ask a follow-up using the interactive tool before finalizing the document.
- Do not emit tool-call JSON, schemas, or internal tool names to the user.
- If the harness has **no interactive input capability**, fall back to concise plain-text questions.

### Example decision mapping

| Missing information | Preferred control |
| --- | --- |
| “Can approver Approve only, or Approve + Reject?” | Single-select |
| “Which roles participate in this process?” | Multi-select when candidate roles are known |
| “What is the exact status name after approval?” | Free-text |
| “How should a mismatch be handled?” with known valid alternatives | Single-select + Other |
| “Describe the current manual process.” | Free-text |

The purpose of the interview is to collect authoritative business decisions, not to make the interaction look polished. Structured UI must never be used to disguise an assumption as a user choice.

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
