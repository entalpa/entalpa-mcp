---
name: entalpa-implement
description: Use this skill when working with Entalpa through its MCP server to implement stories and requirements that were authored on the Entalpa website, inspect the project/stakeholder/story/requirement/subsystem hierarchy, record code references, implementation status, and test coverage back onto requirements, or otherwise perform requirements-engineering work that should preserve traceability and avoid destructive MCP tool calls.
license: MIT
---

# Entalpa Implement

Entalpa is a requirements-engineering platform. In the normal workflow, a human authors project context — the project idea, stakeholders, stories, and story suggestions — **on the Entalpa website**, and generates system requirements and (where the project is decomposed) subsystem requirements from those stories there too. **You, the coding agent, come in after that**: you read the resulting hierarchy over MCP, implement the corresponding code and tests, and write structured feedback (code reference, implementation status, tests) back onto each requirement so the website reflects real progress.

Default to that division of labor: prefer reading and implementing over authoring new stories or requirements. Only create or edit stories/requirements yourself when the user explicitly asks you to draft them.

## Entity Hierarchy

`Project → Stakeholders & Stories → Requirements (system-level) → Subsystems → Requirements (subsystem-level) → Interface Contracts`. Read `references/entity-model.md` for the full model, including how subsystem-level requirements trace back to their parent system requirement, and how content is validated. Subsystems and interface contracts are optional — not every project is decomposed yet.

## Core Workflow — Implementing a Story

1. Confirm authentication with `users_get_me`, then select the project with `projects_list`/`projects_get`. If more than one project could match, ask the user before writing anything.
2. Identify the target story. If the user didn't name one, use `stories_list` to find candidates. Do not create or refine stories yourself unless asked — that normally happens on the website, including AI-generated story suggestions.
3. Call `requirement_items_list` with `story_ids: [story_id]` to get the system-level and, if generated, subsystem-level requirements traced to that story. Story filters deliberately exclude generated interface-requirement rows because interface contracts have no direct story link. If interface context matters, collect the returned subsystem IDs and query `requirement_items_list` again with `kind: "interface_requirement"` and those `subsystem_ids`, or call `interface_contracts_list`.
4. If nothing comes back, the story likely hasn't been propagated to requirements yet. Tell the user to generate (and, if relevant, decompose to subsystems) requirements for that story on the Entalpa website before you implement anything untraceable — don't invent unlinked requirements to fill the gap.
5. For each requirement, check `content.implementation_status` (see `references/implementation-feedback.md`) and skip anything already `implemented`/`verified` unless asked to redo it. Prefer implementing at the most specific level available (a subsystem-level requirement) over its system-level parent when both exist.
6. Implement the change and its tests, then patch the requirement's `implementation_status`, `code_reference`, and `tests` per `references/implementation-feedback.md`. A content patch merges with existing content server-side, so you don't need to re-fetch the requirement first just to preserve its other fields.
7. Summarize: requirement IDs touched, their new status, code/test references, and anything still missing (e.g. "no subsystem requirements exist yet for Billing — generate them on the website").

## Other Workflows (Creating/Reviewing Requirements)

For the less common case where the user asks you to draft stories or requirements yourself, or review coverage, follow the same read-before-write discipline:

- Read `projects_get` and the relevant `stories_list` / `requirements_list` before changing data; read `stakeholders_list`, `subsystems_list`, `interface_contracts_list`, or `projects_get_assessment` when the task depends on those dimensions.
- Plan changes in terms of requirement IDs, source story IDs, acceptance criteria, risk, rationale, and affected components.
- Prefer patch tools over full-object update tools, and prefer updates over delete/recreate.
- Summarize the result with affected IDs, traceability links, assumptions, and any follow-up questions.

## Reference Loading

- Read `references/entity-model.md` to understand the project/stakeholder/story/requirement/subsystem/interface-contract hierarchy and content validation rules.
- Read `references/implementation-feedback.md` before writing `implementation_status`, `code_reference`, or `tests` back onto a requirement.
- Read `references/tool-workflows.md` before making MCP write calls or when choosing which Entalpa tools to use.
- Read `references/requirements-style.md` when creating, rewriting, or reviewing requirement content.
- Read `references/safety-and-traceability.md` before destructive actions, broad updates, or ambiguous project selection.

## Requirement Creation Defaults

When creating a requirement, include a `content` object with:

- `statement`: clear, testable requirement text.
- `acceptance`: measurable completion criteria.
- `rationale`: why the requirement exists.
- `risk`: consequence if it is missed or implemented incorrectly.
- `source`: short provenance note.
- `category`, `component`, and `priority` when known.

Set `source_story_ids` when the requirement is derived from one or more stories. Do not invent story IDs; read stories first and ask when traceability is unclear.

## Destructive Tools

Treat these as destructive: `projects_delete`, `requirements_delete`, `stories_delete`, `stakeholders_delete`, `subsystems_delete`, and `interface_contracts_delete`.

Use destructive tools only when the user explicitly asks for deletion and confirms exact target IDs. When in doubt, produce a proposed deletion list instead of calling the tool.

## State-Changing Confirmation

Use `projects_import` only when the user explicitly asks to create a project from an export. Confirm the source payload and intended project name before importing; do not treat import as a read or backup operation.

Use `projects_undo` and `projects_redo` only when the user explicitly asks to revert or replay project changes. Confirm the exact project ID first, verify `can_undo` or `can_redo` from project state, and summarize the operation before calling the tool.
