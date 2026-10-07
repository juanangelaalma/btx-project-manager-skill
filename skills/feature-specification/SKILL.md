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
