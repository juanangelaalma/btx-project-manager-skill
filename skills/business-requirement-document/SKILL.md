---
name: business-requirement-document
description: "Create or revise a Business Requirements Document (BRD) for software or business-process projects. Use when project objectives need to be decomposed into business actors, scope, rules, requirements, exceptions, traceability, success criteria, and unresolved decisions before detailed business processes or features are specified."
---

# Business Requirements Document

Create a source-grounded BRD that defines **what the business needs and why**, without prematurely specifying implementation details.

## Core Principles

- Never invent process rules, actors, statuses, approvals, tolerances, ownership, accounting treatment, or edge-case behavior.
- When a requirement is ambiguous, interview the user or mark it as an Open Question.
- Existing upstream documents control the business context unless the user explicitly changes them.
- A BRD defines business requirements, not UI design, database schema, API contracts, or engineering tasks.
- Preserve the user's business vocabulary.
- Explicitly record exceptions and unresolved decisions. Do not hide uncertainty inside polished prose.

## Required Upstream Context

Prefer to read the Project Charter before creating a BRD.

Extract and preserve:

- project objectives,
- scope boundaries,
- business entities,
- stakeholders,
- constraints,
- success criteria.

If no Project Charter exists, ask for enough context to reconstruct the relevant baseline without pretending one exists.

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

Before drafting, determine whether these are materially clear:

1. business process/domain covered,
2. business problem and objective,
3. actors and responsibilities,
4. start and end boundaries,
5. main happy path,
6. approvals and decision points,
7. business rules,
8. key exceptions/variance scenarios,
9. business statuses/lifecycle where relevant,
10. transaction/document relationships,
11. upstream/downstream dependencies,
12. reporting/traceability expectations,
13. unresolved decisions.

Ask targeted questions only for material gaps. Do not ask implementation questions unless they affect business behavior.

## Workflow

### 1. Read and reconcile upstream sources

Identify which source is authoritative. If a newer user clarification conflicts with an older document, treat the newer explicit clarification as the proposed change and update the BRD only after confirming it is intentional.

### 2. Define process boundary

State where this BRD starts and ends. Explicitly identify neighboring processes that are outside scope.

### 3. Identify actors and responsibilities

Use business roles, not guessed job titles. Avoid combining distinct responsibilities merely for convenience.

### 4. Capture high-level business flow

Describe the end-to-end flow at business level. This is not yet a detailed BPMN specification.

### 5. Write atomic business requirements

Each requirement should:

- express one business need,
- be testable or verifiable,
- avoid implementation-specific wording unless required by the business,
- have a stable ID such as `BR-[DOMAIN]-001`.

### 6. Define business rules and exceptions

Separate normative rules from exception scenarios. Include concrete examples when they reduce ambiguity.

### 7. Define lifecycle and traceability

Where transactions have meaningful states, document the proposed lifecycle. If status names are not final, say so.

Define forward and backward traceability between business documents where relevant.

### 8. Record Open Questions

Every unresolved decision gets:

- ID,
- question,
- current direction or known context,
- status.

Remove questions once answered and move the resulting decision into the relevant requirement/rule.

### 9. Run contradiction scan

Search the complete draft for legacy or conflicting rules. Common contradictions include:

- automatic vs manual action,
- actor ownership mismatch,
- reject allowed vs reject forbidden,
- cancellation vs replacement,
- stock ownership/status inconsistencies,
- one-to-one vs one-to-many document relationships,
- Closed questions still appearing in Open Questions.

## Required Output Structure

```markdown
# BRD – [Business Process / Domain]

## 1. Document Information
## 2. Business Background
## 3. Business Objectives
## 4. Actors & Stakeholders
## 5. Scope
### In Scope
### Out of Scope / Deferred
## 6. High-Level Business Flow
## 7. Business Requirements
## 8. Business Rules
## 9. Exception & Variance Scenarios
## 10. Fulfillment / Tracking / Monitoring
## 11. Proposed Status Lifecycle
## 12. Traceability Requirements
## 13. Business Success Criteria
## 14. Open Questions / Decision Log Candidates
## 15. Future Breakdown
## 16. Approval / Baseline
```

Adapt sections to the domain rather than forcing irrelevant sections.

## Requirement Style

Use:

```markdown
### BR-P2P-012 – Manual Stock Transfer
The system must allow authorized HO users to initiate stock transfer to a branch manually after the preceding business condition is satisfied.
```

Avoid vague requirements such as:

- “system should be flexible”,
- “support normal business process”,
- “handle errors properly”.

## Scope Discipline

When reviewing external feedback or generic ERP recommendations, classify each proposal as:

- Adopt
- Deferred
- Not Applicable
- Needs Stakeholder Clarification

Do not turn “common industry practice” into a requirement without evidence that the business needs it.

## Quality Gate

Before finalizing, verify:

- all requirements trace to project/business objectives,
- no unsupported facts were invented,
- every actor has a meaningful responsibility,
- high-level flow and business rules agree,
- status lifecycle matches the described process,
- document cardinalities are explicit where material,
- exceptions do not contradict the happy path,
- answered Open Questions are removed,
- future breakdown can cleanly feed Business Process and Feature work.

## Handoff

Recommend creating one Business Process document per meaningful sub-process. Each Business Process must reference the BRD requirements it implements.
