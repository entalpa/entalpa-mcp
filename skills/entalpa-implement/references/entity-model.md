# Entalpa Entity Model

Use this reference to understand how Entalpa project data is organized before reading or writing anything through MCP.

## Hierarchy

```
Project
├─ Stakeholders  ──┐  (many-to-many: a story can involve several stakeholders)
├─ Stories       ──┘
│    └─ Requirements            (system-level: subsystem_id is absent/null)
│         └─ Requirements       (subsystem-level: subsystem_id is set)
├─ Subsystems
│    └─ owns every subsystem-level Requirement whose subsystem_id matches it
└─ Interface Contracts          (DATA / TRIGGER / STATE boundary between two Subsystems)
```

- **Project** — the root container. Holds `title`, `design_description`, `messages` (chat history), `assessment_score`/`assessment_details`, and `extra_requirement_attributes` (see below).
- **Stakeholders** and **Stories** are siblings directly under the project. A stakeholder links to the stories it cares about (`story_ids`); a story links back to its stakeholders (`stakeholder_ids`).
- **Requirements** are not children of stories in a strict tree — they are linked to one or more stories via `source_story_ids`. A requirement with no `subsystem_id` is a **system-level requirement**: it describes behavior of the system as a whole and should trace to at least one story.
- **Subsystem-level requirements** are the same `Requirement` object type, distinguished only by having `subsystem_id` set. Instead of tracing to stories directly, they trace to the system-level requirement(s) they refine via `source_requirement_ids` (a self-referential link). `parent_requirements` (`{id, human_id}`) is a computed convenience view of that same link.
- **Subsystems** are the architectural components a project is decomposed into. A subsystem owns the subsystem-level requirements whose `subsystem_id` points to it.
- **Interface Contracts** describe a boundary between exactly two subsystems (`source_subsystem_id` → `target_subsystem_id`) with an `interface_type` of `DATA`, `TRIGGER`, or `STATE`. They are the formal way one subsystem's requirements depend on another's.

Not every project has subsystems yet. Treat subsystem-level requirements and interface contracts as optional refinements that may not exist if the project hasn't been decomposed on the Entalpa website.

## Tracing a Story End to End

Pass `story_ids: [story_id]` to `requirement_items_list` to fetch the system-level and subsystem-level requirements traced to a story. Interface contracts do not carry direct story links, so the API excludes generated `interface_requirement` rows whenever a story or stakeholder filter is present. To inspect interface context, collect the subsystem IDs from the story-linked requirements and make a second call with `kind: "interface_requirement"` and those `subsystem_ids`, or call `interface_contracts_list`. See `references/tool-workflows.md` for the exact pattern.

## Content Is Free-Form, With One Constraint

`Requirement.content` (and `InterfaceContract.content`) is a JSON object. Common keys — `id`, `source`, `statement`/`requirement`, `acceptance`, `rationale`, `risk`, `guidance`, `priority`, `category`, `component` — are conventional, not enforced individually. However, the server validates the object shape: **every key's value must be a plain string or a list of strings.** Nested objects or numbers as values will be rejected. Keep this in mind whenever you add a new key, including the implementation-feedback keys described in `references/implementation-feedback.md`.

`Project.extra_requirement_attributes` is a separate, project-level list drawn from a fixed enum (`rationale`, `acceptance`, `risk`, `guidance`, `priority`, `category`, `component`). It controls which of those *descriptive* fields the project's own requirement-generation prompts fill in — it has nothing to do with implementation-feedback keys, which live purely as extra keys in `content` that you add yourself.

## Versions and Diffs

Entalpa keeps project snapshots and can diff two versions. `projects_list_snapshots` and `projects_diff` are MCP tools — use them to find out "what's new since I last looked" instead of re-reading everything and diffing client-side. MCP has no explicit create-snapshot tool; snapshots are recorded automatically as project changes are committed, including changes made through MCP write tools. See `references/tool-workflows.md` for the exact call pattern.

## Portable Export/Import

`projects_export` returns a project (subsystems, stakeholders, stories, requirements, interface contracts) as a single portable JSON object; `projects_import` takes that object back and creates a new project from it. Use these for cloning or backing up a project, not for routine reads — every other tool above is cheaper and more targeted for day-to-day work.
