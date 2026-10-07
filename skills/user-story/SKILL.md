---
name: user-story
description: "Create or revise implementation-ready User Stories from Feature, Business Process, and BRD sources. Use when a defined business capability must be decomposed into user outcomes with acceptance criteria, rules, edge cases, dependencies, traceability, and clear readiness for engineering work."
---

# User Story

Create user-centered, testable User Stories that implement an approved Feature without introducing unsupported business rules.

## Core Principles

- Never invent business behavior, permissions, statuses, validation, or exceptions.
- Read the Feature first, then Business Process and BRD as needed.
- A User Story expresses a user/business outcome, not an engineering task.
- Acceptance Criteria must be observable and testable.
- One story should have one primary outcome.
- When the upstream documents are ambiguous, stop and clarify or mark the story Blocked/TBD.

## Required Upstream Context

Prefer this order:

1. Feature specification,
2. Business Process,
3. BRD,
4. Project Charter only for high-level scope checks.

Never use a lower-level story to override an upstream business decision silently.

## Interview Gate

Clarify material unknowns such as:

- primary actor,
- user goal,
- trigger/precondition,
- successful outcome,
- validation/business rules,
- permissions,
- status transition,
- exception behavior,
- dependency on another story.

Do not ask for UI details unless they are genuinely business requirements.

## Workflow

### 1. Select a vertical story slice

Prefer a complete user outcome.

Good:
`As HO Purchasing, I want to submit a completed PO for approval so that the purchase can be formally authorized.`

Bad:
`As a developer, I want an approval table.`

### 2. Validate source traceability

Identify:

- Feature section,
- Business Process step(s),
- BRD requirement ID(s).

If traceability is missing, flag the gap.

### 3. Write the story statement

Default format:

```markdown
As a [business actor],
I want [capability/action],
so that [business outcome/value].
```

Use another format only if it communicates the requirement more clearly.

### 4. Write Acceptance Criteria

Prefer Given/When/Then when behavior has conditions or state changes.

```markdown
Given ...
When ...
Then ...
```

For simple criteria, a testable checklist is acceptable.

Acceptance Criteria should cover:

- happy path,
- mandatory validation,
- relevant permissions,
- relevant status change,
- material exception or variance behavior.

Do not stuff every possible edge case into one story.

### 5. Separate business acceptance from technical work

Do not include implementation tasks such as migrations, API endpoints, unit tests, or frontend components inside Acceptance Criteria unless the user explicitly requests technical criteria.

### 6. Check story size

Split the story when it contains multiple independent outcomes, unrelated actors, or several distinct lifecycle transitions that can be delivered separately.

## Required Output Structure

```markdown
# User Story – [Story Title]

## Story ID
US-[DOMAIN]-[NNN]

## Parent Feature
[Feature reference]

## User Story
As a ...
I want ...
So that ...

## Business Context

## Preconditions

## Acceptance Criteria
### AC-01 – [Scenario]
Given ...
When ...
Then ...

## Business Rules

## Exceptions / Edge Cases

## Status Transition

## Dependencies

## Traceability
- BRD: BR-...
- Business Process: ...
- Feature: ...

## Out of Scope

## Open Questions

## Definition of Ready
```

Omit irrelevant sections only when clearly unnecessary.

## Acceptance Criteria Rules

Acceptance Criteria must be:

- specific,
- testable,
- business-observable,
- internally consistent,
- traceable to upstream requirements.

Avoid:

- `system works correctly`,
- `UI should be user friendly`,
- `handle all errors`,
- implementation details with no business rationale.

## Story Splitting Heuristics

Split by:

- workflow stage,
- actor outcome,
- business rule variation,
- happy path vs materially separate exception workflow,
- independent lifecycle transition.

Do not split only by technical layer.

## Definition of Ready

A story is ready for technical breakdown when:

- actor and outcome are clear,
- parent Feature is known,
- Acceptance Criteria are testable,
- permissions/status behavior is known when relevant,
- dependencies are identified,
- no unresolved question blocks implementation.

If a blocking question remains, explicitly mark the story as not ready.

## Quality Gate

Before finalizing:

- no unsupported rule was invented,
- story has one primary outcome,
- Acceptance Criteria are testable,
- business rule and status behavior agree with upstream docs,
- edge cases are proportionate to the story,
- technical tasks have not been mixed into the story,
- traceability is complete.

## Handoff

After the story is ready, it may be decomposed into engineering tasks, test cases, and implementation design. Those are downstream artifacts and should not be silently embedded into the User Story.
