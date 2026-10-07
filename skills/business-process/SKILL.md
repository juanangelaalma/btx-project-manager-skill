---
name: business-process
description: "Create or revise a detailed Business Process document from an approved or draft BRD. Use when a business requirement needs actor-by-actor flow, triggers, preconditions, steps, decisions, exceptions, statuses, outputs, traceability, and optionally BPMN 2.0 XML after explicit clarification with the user."
---

# Business Process

Translate BRD requirements into an unambiguous business flow that explains **who does what, when, under which conditions, and what happens next**.

## Core Principles

- Never invent missing branches, approvals, exceptions, statuses, ownership, or system behavior.
- Read the relevant BRD before drafting whenever available.
- Business Process may refine flow detail but must not silently create new business requirements.
- If a new rule is discovered, identify it as a BRD gap and ask whether the BRD should be updated.
- Keep business behavior separate from technical implementation.
- BPMN XML is optional and must not be generated automatically. Ask the user whether BPMN XML is desired once the narrative flow is sufficiently clear.

## Required Upstream Context

Read:

1. Project Charter when relevant,
2. BRD for the domain/process,
3. any existing decision log or SOP referenced by the BRD.

Extract:

- relevant BR IDs,
- actors,
- business rules,
- status lifecycle,
- exceptions,
- open questions.

## Interview Gate

Before drafting a process, clarify material unknowns such as:

- trigger,
- start/end event,
- primary actor,
- supporting actors,
- approval behavior,
- decision/gateway conditions,
- exception paths,
- status transitions,
- cancellation/replacement/reversal behavior,
- upstream/downstream dependencies.

Do not ask about information already defined in the BRD.

## Workflow

### 1. Select one process boundary

One document should represent one coherent process or sub-process. Avoid giant documents containing unrelated processes.

### 2. Map actors to responsibilities

For each step, ensure an accountable actor exists.

### 3. Define trigger, preconditions, and inputs

Do not confuse a trigger with a precondition.

Example:

- Trigger: approved request requires purchase execution.
- Precondition: supplier master exists.

### 4. Write the main flow

Use numbered steps. Each step should include:

- actor,
- action,
- resulting state/output when relevant.

### 5. Define decision points

For every branch, state the condition explicitly.

Bad:
`If invalid, handle accordingly.`

Good:
`If received quantity is lower than ordered quantity, record actual received quantity and keep the remaining quantity outstanding.`

### 6. Define alternative and exception flows

Include only supported scenarios. If behavior is unknown, create an Open Question rather than inventing a route.

### 7. Define state transition

Where state matters, provide a table:

```markdown
| Current Status | Action | Actor | Next Status |
```

### 8. Verify BRD traceability

List the BR IDs implemented by this process. If a process rule has no BRD source, flag it.

### 9. Offer BPMN only after narrative is stable

Ask:

> “Flow naratifnya sudah cukup jelas. Apakah ingin saya buatkan BPMN 2.0 XML yang dapat diimpor ke bpmn.io?”

If user says yes:

- clarify unresolved gateways/exceptions first,
- use valid BPMN 2.0 semantics,
- define Pool/Lanes from business participants,
- generate importable XML,
- never encode an unresolved business rule as if final.

## Required Narrative Output Structure

```markdown
# Business Process – [Process Name]

## 1. Process Information
## 2. Purpose / Objective
## 3. Trigger
## 4. Preconditions
## 5. Actors & Responsibilities
## 6. Inputs
## 7. Main Business Flow
## 8. Decision Points / Gateways
## 9. Business Rules
## 10. Alternative & Exception Flows
## 11. Status Lifecycle / Transition
## 12. Outputs
## 13. Upstream & Downstream Dependencies
## 14. Related BRD Requirements
## 15. Open Questions
## 16. Process Boundary
```

Adapt sections only when useful.

## Swimlane Guidance

When useful, include a textual swimlane matrix in Markdown:

```markdown
| Actor / Lane | Step 1 | Step 2 | Step 3 |
```

Use it to clarify handoffs, not as a substitute for the narrative process.

## BPMN Guardrails

If BPMN is requested:

- use Start/End Events appropriately,
- use User/Service/Manual Tasks only when semantics are known,
- use Exclusive/Parallel gateways only when business logic supports them,
- avoid decorative gateways,
- ensure sequence flows do not cross Pool boundaries incorrectly,
- use Message Flows for cross-participant communication,
- keep lane ownership aligned with narrative actors,
- validate that every gateway has understandable outgoing conditions,
- preserve unresolved cases as notes/open questions, not fabricated BPMN paths.

## Quality Gate

Before finalizing:

- every step has an actor,
- every branch has a condition,
- no step contradicts the BRD,
- all significant statuses are represented,
- exceptions are supported by source requirements,
- process start and end are clear,
- downstream process handoff is explicit,
- no technical design leaked into the business process without need.

## Handoff

Once stable, the process can be decomposed into Features. Features should represent coherent user/business capabilities rather than individual process steps.
