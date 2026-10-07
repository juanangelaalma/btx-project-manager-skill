# BTX Project Manager Skills

Reusable Agent Skills for project and product documentation workflows.

This repository contains five source-grounded skills that form a documentation chain:

```
Project Charter
      ↓
Business Requirements Document (BRD)
      ↓
Business Process
      ↓
Feature Specification
      ↓
User Story
```

The skills are generic and can be used across software and business projects. They are intentionally strict about source grounding: **the agent must not invent missing business requirements**. When material information is missing, the agent should interview the user or surface an explicit Open Question.

## Included Skills

| Skill | Purpose |
|---|---|
| `project-charter` | Establish project purpose, objectives, scope, governance, risks, milestones, and success criteria. |
| `business-requirement-document` | Turn project objectives into business requirements, rules, exceptions, lifecycle, and traceability. |
| `business-process` | Turn BRD requirements into actor-by-actor business flows, decisions, states, exceptions, and optional BPMN 2.0 XML. |
| `feature-specification` | Define a coherent business/product capability before decomposing it into User Stories. |
| `user-story` | Create traceable, testable User Stories and Acceptance Criteria from upstream documentation. |

## Repository Structure

```text
btx-project-manager-skill/
├── README.md
└── skills/
    ├── project-charter/
    │   └── SKILL.md
    ├── business-requirement-document/
    │   └── SKILL.md
    ├── business-process/
    │   └── SKILL.md
    ├── feature-specification/
    │   └── SKILL.md
    └── user-story/
        └── SKILL.md
```

Each skill follows the Agent Skills convention: a directory containing a `SKILL.md` file with YAML frontmatter containing at least `name` and `description`.

## Install

The easiest way to install is with the open Agent Skills CLI.

### Install interactively

```bash
npx skills add juanangelaalma/btx-project-manager-skill
```

The CLI will discover the five skills and let you choose which ones to install.

### List available skills first

```bash
npx skills add juanangelaalma/btx-project-manager-skill --list
```

### Install all skills

```bash
npx skills add juanangelaalma/btx-project-manager-skill --skill '*'
```

To install all skills into every detected agent harness:

```bash
npx skills add juanangelaalma/btx-project-manager-skill --all
```

### Install one skill

Example: install only the BRD skill.

```bash
npx skills add juanangelaalma/btx-project-manager-skill \
  --skill business-requirement-document
```

You can repeat `--skill` to install several skills:

```bash
npx skills add juanangelaalma/btx-project-manager-skill \
  --skill project-charter \
  --skill business-requirement-document \
  --skill business-process
```

### Install for a specific agent harness

Examples:

```bash
# Claude Code
npx skills add juanangelaalma/btx-project-manager-skill \
  --skill '*' \
  --agent claude-code

# Codex
npx skills add juanangelaalma/btx-project-manager-skill \
  --skill '*' \
  --agent codex

# OpenCode
npx skills add juanangelaalma/btx-project-manager-skill \
  --skill '*' \
  --agent opencode
```

The Agent Skills CLI supports many other compatible harnesses as well. Run:

```bash
npx skills --help
```

to inspect the options supported by your installed CLI version.

### Install globally

By default, skills are installed for the current project. To make them available globally:

```bash
npx skills add juanangelaalma/btx-project-manager-skill \
  --skill '*' \
  --global
```

or the short form:

```bash
npx skills add juanangelaalma/btx-project-manager-skill -g
```

### Non-interactive install

Useful for onboarding scripts or CI:

```bash
npx skills add juanangelaalma/btx-project-manager-skill \
  --skill '*' \
  --agent claude-code \
  --yes
```

## Install Directly From a Skill Path

You can also install a single skill directly from GitHub:

```bash
npx skills add \
  https://github.com/juanangelaalma/btx-project-manager-skill/tree/master/skills/business-process
```

Replace `business-process` with any skill directory.

## Verify Installation

First, ask the CLI to list the skills it can discover:

```bash
npx skills add juanangelaalma/btx-project-manager-skill --list
```

You should see:

```text
project-charter
business-requirement-document
business-process
feature-specification
user-story
```

You can also inspect the skill directory used by your agent. The exact path depends on the harness and whether the install is project-local or global.

## Recommended Usage

Use the skills in order whenever possible.

### 1. Project Charter

Example prompt:

```text
Use the project-charter skill.

I am starting an accounting application project.
Interview me first for any material information that is missing.
Do not invent owners, scope, dates, or success metrics.
Then create the Project Charter in Markdown.
```

### 2. Business Requirements Document

```text
Use the business-requirement-document skill.

Read the Project Charter first.
Help me define the Procure-to-Pay BRD.
Interview me where the business behavior is unclear.
Do not infer business rules from generic ERP practices.
```

### 3. Business Process

```text
Use the business-process skill.

Read the BRD first and create the Purchase Order Business Process.
Clarify unresolved decisions before writing the final flow.
After the narrative flow is stable, ask me whether I want BPMN 2.0 XML.
```

### 4. Feature Specification

```text
Use the feature-specification skill.

Read the BRD and Business Process first.
Create Feature specifications for the approved Purchase Order process.
Do not create features that are unsupported by upstream requirements.
```

### 5. User Story

```text
Use the user-story skill.

Read the Feature, Business Process, and BRD.
Create implementation-ready User Stories with Given/When/Then Acceptance Criteria.
Do not invent validations, permissions, status transitions, or edge cases.
```

## Design Principles

These skills follow several strict rules:

1. **Interview before inventing.** If a missing answer materially changes the document, ask.
2. **Source hierarchy matters.** Downstream artifacts must not silently override upstream business decisions.
3. **Traceability is required.** BRD → Business Process → Feature → User Story should remain traceable.
4. **Open questions stay visible.** Unknowns must not disappear inside polished prose.
5. **Markdown-first.** The skills produce portable Markdown documentation.
6. **Business before implementation.** UI, database, API, and engineering tasks should not leak into business artifacts unless specifically required.
7. **BPMN is opt-in.** The Business Process skill only generates BPMN XML after the user confirms the narrative flow and explicitly wants BPMN.

## Interactive Interview UX

All five skills are designed to use the **native interactive input capability of the active agent harness** whenever it is available.

Instead of dumping a plain-text questionnaire such as:

```text
1. Who approves the PO?
2. Can it be rejected?
3. What is the next status?
```

the skill instructs the agent to prefer structured controls:

| Question type | Preferred UI |
|---|---|
| One known choice | Single-select / options |
| Several applicable choices | Multi-select / checkboxes |
| Unknown factual value | Free-text / text field |
| Known choices plus custom business behavior | Options + Other/free-text |

This is intentionally **harness-agnostic**. Claude Code, Codex, OpenCode, and other harnesses may expose different tool names or UI controls. The skill does not hard-code one provider's tool name. It tells the agent to use whichever native structured-question/input tool is available.

If the harness does not expose interactive input tools, the skill falls back to concise plain-text clarification questions.

Important behavior:

- only ask material questions,
- usually ask 1–3 related questions per round,
- do not ask again for facts already known,
- do not offer “You decide” for factual business decisions,
- do not invent a value when a text field should be used,
- keep recommendations separate from answer choices.


## Updating Installed Skills

Agent Skills CLI behavior can evolve. A reliable way to refresh a skill is to run the install command again against this repository. If your CLI version provides an update command, you can also use that.

## Requirements

- Node.js with `npx`
- A compatible Agent Skills harness

No project-specific runtime dependency is required by the skills themselves.

## License

Add the license appropriate for your organization before redistributing under a specific license.
