# Entalpa MCP Tool Workflows

Use this reference before MCP write calls or when choosing which Entalpa tools to call.

## Project Selection

1. Call `users_get_me` to confirm the authenticated user.
2. Call `projects_list` with a reasonable limit.
3. If the user named a project, match by exact title first, then clear substring match.
4. If no project is unambiguous, ask the user to choose. Do not write to a guessed project.
5. Call `projects_get` for the selected project before inspecting or changing requirements.

## Read Context

Use these tools to build context:

- `projects_get`: project metadata and description.
- `projects_get_assessment`: readiness and quality assessment when planning gaps or prioritization.
- `projects_get_messages`: prior project conversation context when reconstructing intent.
- `stories_list` / `stories_get`: source stories for traceability.
- `requirements_list` / `requirements_get`: existing requirement set.
- `requirement_items_list`: combined requirement and interface requirement view.
- `stakeholders_list` / `stakeholders_get`: actors and stakeholder needs.
- `subsystems_list` / `subsystems_get`: affected system components.
- `interface_contracts_list` / `interface_contracts_get`: boundaries, payloads, triggers, and state interfaces.
- `project_search`: case-insensitive substring search across stories, requirements, stakeholders, subsystems, and interface contracts — use it instead of listing everything and filtering client-side.
- `resolve_ids`: bulk-map references (human ids like `Req-012`/`S-3`, UUIDs, or stakeholder names) to entities in one call.
- `requirements_get_many` / `stories_get_many`: fetch several entities by UUID and/or human id in one call.
- `projects_list_snapshots` / `projects_diff`: list saved snapshots and diff project versions (see below).

## Transfer Projects

- `projects_export` is non-mutating. Use it to produce a portable JSON backup or transfer payload.
- `projects_import` creates a project from a portable JSON payload. Call it only when the user explicitly asks to import or clone a project, after confirming the payload and intended project name.

## Human ids and lookups

Everything a human references is a human id — `Req-012` (a requirement's `content.id`), `S-3` (story), `Sub-002` (subsystem), `REQ-INT-001` (interface contract) — or, for stakeholders, a name. You do not need to resolve these to UUIDs first:

- `*_get`/`*_update`/`*_patch`/`*_delete` for requirements, stories, subsystems, and interface contracts accept `human_id` in place of the UUID id; stakeholder get/delete accept `name`. Provide one form; giving both with a mismatch is rejected.
- Use `project_search` to find an entity by text, or `resolve_ids` to map a batch of references at once and see which ones don't exist.

## Trace a Story to Its Requirements

Use `requirement_items_list` with `story_ids: [story_id]` to fetch the system-level and, if the project has been decomposed, subsystem-level requirements derived from a story. These rows have `kind: "requirement"`; use `subsystem_id`/`subsystem_ids` to distinguish system-level rows from subsystem-level rows.

Story and stakeholder filters deliberately exclude generated `interface_requirement` rows because interface contracts have no direct story link. If the implementation needs interface context, collect the subsystem IDs from the story-linked requirements and make a second `requirement_items_list` call with `kind: "interface_requirement"` and those `subsystem_ids`, or call `interface_contracts_list`. Generated interface rows are read-only views; update their underlying contracts with `interface_contracts_patch`.

This is the mechanism for finding requirements that were already propagated from a story — there is no separate propagation tool to call. The requirements exist once generated on the website, and these list calls are how you discover them.

If the call returns nothing for a story, requirements haven't been generated for it yet. Ask the user to generate them on the Entalpa website rather than fabricating unlinked requirements.

## Find What Changed (Snapshots & Diff)

To implement "only what's new" after the user extends a project: call `projects_list_snapshots` to find a baseline snapshot, then `projects_diff` with `base: <snapshot_id>` (and `compare` defaulting to `current`). The result groups stories, requirements, and interface contracts into `added` / `removed` / `modified` / `unchanged` buckets, keyed by human id — implement the `added` and `modified` requirements. MCP has no explicit create-snapshot tool; snapshots are recorded automatically when project changes are committed, including through MCP write tools.

You can also narrow `requirement_items_list` server-side instead of fetching everything and filtering client-side: `story_ids`/`stakeholder_ids`/`subsystem_ids` (UUIDs or human ids/names), `kind` (`requirement` vs `interface_requirement`), `flags`, or a `content_key` (optionally with `content_contains`) — e.g. `{content_key: "implementation_status", content_contains: "progress"}`.

## Update Project Metadata

- Prefer `projects_patch` for partial project metadata edits.
- Use `projects_update` only when replacing the full project object intentionally. Before `projects_update`, call `projects_get` and include every field that should be preserved.
- Use `projects_undo` and `projects_redo` only when the user asks to revert or replay Entalpa project changes. Confirm the exact project ID and verify `can_undo` or `can_redo` before calling.

## Create Requirements

Use `requirements_create` with:

- `project_id`
- `requirement.content.statement`
- `requirement.content.acceptance`
- `requirement.content.rationale`
- `requirement.content.risk`
- `requirement.content.source`
- `requirement.source_story_ids` when known
- `requirement.flags`, `lock`, or `from_description` only when the user intent or existing project pattern calls for them

Prefer server-generated content IDs unless the project already uses a clear naming convention.

## Update Requirements

- Use `requirements_patch` for partial edits.
- Prefer `requirements_patch` for normal requirement edits.
- Use `requirements_update` only when replacing the full requirement object intentionally. It can reset omitted fields such as `source_story_ids`, `flags`, and `lock` to defaults.
- Before `requirements_update`, call `requirements_get` and include every field that should be preserved, including `source_story_ids`, `flags`, `lock`, and all existing `content` fields.
- The `content` object itself is the exception: whatever `content` you send in `requirements_patch` or `requirements_update` is shallow-merged with the requirement's existing `content` server-side. A patch of `{"content": {"implementation_status": "implemented"}}` does not require re-fetching the requirement first to preserve `statement`, `acceptance`, etc. — see `references/implementation-feedback.md`.
- Re-read the updated requirement when the result needs confirmation.

## Related Objects

- Use `stories_create` or `stories_update` only when the user asks to add or change stories, or when requirement creation depends on a missing story and the user approves creating it.
- Use `stakeholders_create`, `subsystems_create`, `subsystems_update`, or interface-contract write tools only when the task explicitly touches those objects.
- Before `subsystems_update`, call `subsystems_get` and include every existing subsystem field that should be preserved.
- Prefer `interface_contracts_patch` for interface-contract edits. Before `interface_contracts_update`, call `interface_contracts_get` and include every field that should be preserved, including `content`, `flags`, and `lock`.

## Final Response Pattern

End with:

- Project name and ID.
- Created or updated requirement IDs.
- Source story IDs linked to each requirement.
- Assumptions or missing context.
- Any destructive actions performed, if any.
