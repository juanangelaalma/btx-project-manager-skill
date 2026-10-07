---
name: feature-specification
description: "Create or revise a Feature specification from BRD and Business Process documents. Use when a coherent business capability needs scope, actors, functional behavior, business rules, states, dependencies, edge cases, traceability, and a clear boundary before it is decomposed into User Stories."
---

# Feature Specification

Define a coherent product capability that implements part of a business process and is ready to decompose into User Stories.

## Core Principles

- A Feature is a user/business capability, not a screen, API endpoint, database table, or engineering task.
- Never invent behavior not supported by BRD or Business Process sources.
- Read upstream documents first when available.
- When a needed behavior is missing upstream, flag a gap instead of silently deciding it.
- Keep the Feature large enough to deliver meaningful capability but small enough to decompose into a manageable set of User Stories.

## Required Upstream Context

Prefer to read:

1. relevant BRD,
2. relevant Business Process,
3. Project Charter for scope validation when necessary.

Extract:

- related BR IDs,
- process steps,
- actors,
- business rules,
- status transitions,
- exceptions,
- unresolved questions.

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

Clarify only material gaps such as:

- feature objective,
- intended actors,
- process boundary covered,
- required behaviors,
- important variants,
- permissions/approval behavior,
- states,
- dependencies,
- explicit exclusions.

If upstream sources are incomplete, explain which missing answer blocks the Feature.

## Workflow

### 1. Define the capability

Use a noun phrase that describes business value, for example:

- Multi-Branch Purchase Order
- Goods Receive Verification
- Purchase Invoice Matching

Avoid names such as `PO Page`, `Invoice API`, or `Create Button`.

### 2. Define objective and value

Explain what business outcome this Feature enables and which process segment it supports.

### 3. Set feature boundary

Define:

- Included behavior
- Excluded behavior
- Dependencies

### 4. Describe functional behavior

Describe observable business behavior without prescribing UI architecture.

### 5. Define rules and states

Reference existing BRD/business-process rules rather than duplicating them inconsistently.

### 6. Capture exceptions

Include supported edge cases that materially affect user stories.

### 7. Prepare story decomposition

Identify logical story slices by user outcome, not by technical layer.

Good slices:

- Create multi-branch PO
- Submit PO for approval
- Mark approved PO as sent

Bad slices:

- Build database table
- Build controller
- Build frontend form

## Required Output Structure

```markdown
# Feature – [Feature Name]

## 1. Feature Summary
## 2. Business Objective / Value
## 3. Actors
## 4. Scope
### Included
### Excluded
## 5. Functional Behavior
## 6. Business Rules
## 7. Status / State Behavior
## 8. Exceptions & Edge Cases
## 9. Dependencies
## 10. Data / Document Relationships
## 11. Permissions & Approval Considerations
## 12. Traceability
### Related BRD Requirements
### Related Business Process Steps
## 13. Candidate User Stories
## 14. Open Questions
## 15. Definition of Ready for Story Breakdown
```

## Traceability Contract

Each Feature should reference:

- one or more BRD requirement IDs,
- one or more Business Process sections/steps.

If no upstream requirement supports the Feature, stop and flag the missing business requirement.

## Definition of Ready

A Feature is ready for User Story decomposition when:

- objective is clear,
- actors are known,
- major flow is known,
- business rules are known,
- states are known when relevant,
- important edge cases are known,
- dependencies are understood,
- unresolved questions do not block story acceptance criteria.

## Quality Gate

Before finalizing:

- the Feature represents business capability rather than implementation,
- boundaries do not overlap confusingly with neighboring Features,
- every rule has upstream support,
- candidate stories are independently understandable,
- no acceptance criteria are invented prematurely,
- open questions remain visible.

## Handoff

Use the User Story skill to decompose this Feature into outcome-oriented stories with acceptance criteria grounded in the Feature and upstream process rules.
