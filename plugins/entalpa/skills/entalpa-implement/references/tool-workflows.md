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

- `projects_overview`: read it first. In one call it gives counts of stakeholders, stories, requirements (per category and `lifecycle` status), subsystems and open questions; the gaps that need attention, with a few IDs each; the suggested next step; and the credits AI work on the project has used. It does not list pending suggestions; call `suggestions_list` for those.
- `projects_get`: project metadata and description.
- `projects_get_assessment`: readiness and quality assessment when planning gaps or prioritization.
- `projects_get_messages`: prior project conversation context when reconstructing intent.
- `stories_list` / `stories_get`: source stories for traceability.
- `requirements_list` / `requirements_get`: existing requirement set.
- `requirement_items_list`: combined requirement and interface requirement view.
- `stakeholders_list` / `stakeholders_get`: actors and stakeholder needs. Stakeholders have human IDs like `SH-004`. Stories have them too (`S-001`), and the story tools return them as `human_id`.
- `open_questions_list`: the decisions the spec leaves open, with `status` (`open`, `answered`, `dismissed`) and `story_id` filters. See "Open Questions" below.
- `suggestions_list`: AI proposals waiting for review. See "Saved Suggestions" below.
- `subsystems_list` / `subsystems_get`: affected system components.
- `interface_contracts_list` / `interface_contracts_get`: boundaries, payloads, triggers, and state interfaces.
- `project_search`: case-insensitive substring search across stories, requirements, stakeholders, subsystems, and interface contracts — use it instead of listing everything and filtering client-side.
- `resolve_ids`: bulk-map references (human ids like `Req-012`/`S-3`, UUIDs, or stakeholder names) to entities in one call.
- `requirements_get_many` / `stories_get_many`: fetch several entities using UUIDs in `ids`.
- `projects_list_snapshots` / `projects_diff`: list saved snapshots and diff project versions (see below).

## Transfer Projects

- `projects_export` is non-mutating. Use it to produce a portable JSON backup or transfer payload.
- `projects_import` creates a project from a portable JSON payload. Call it only when the user explicitly asks to import or clone a project, after confirming the payload and intended project name.

## Identity and Lookups

Use human IDs and names in explanations: `Req-012` (a requirement's `content.id`), `S-3` (story), `Sub-002` (subsystem), or a stakeholder's name. Existing-entity tool targets, selections, filters and relationships require UUIDs, including subsystem/interface endpoints and open-question targets.

- Copy the returned entity UUID: list/get tools use fields such as `requirement_id` or `story_id`; search/resolve results use `id`, and combined requirement rows use `item_id`. If only a label is known, call `resolve_ids` with `{project_id, refs: ["Req-012"]}` or use `project_search`. Check the returned entity kind and project before using its UUID; unresolved or ambiguous references need clarification.
- For example, use a resolved requirement's `id` as `requirements_patch.requirement_id`. Do not send `human_id`, `human_ids` or stakeholder `name` as alternative operation selectors. Creation/edit fields such as `content.id`, `human_id` and `name` remain readable labels where the tool schema permits them.
- Retain the selected UUID through the task. A rename does not change the target; if that UUID disappears, stop and ask the user before selecting a replacement, even if its label, wording, and metadata match. Never generate or guess a UUID.
- Project, user and snapshot identifiers are UUIDs too. Portable exports and `projects_diff` deliberately use human-readable document/history IDs; do not pass those IDs as operation targets or assume a historical label still identifies the same current entity.

## Trace a Story to Its Requirements

Use `requirement_items_list` with `story_ids: [story_id]` to fetch the system-level and, if the project has been decomposed, subsystem-level requirements derived from a story. These rows have `kind: "requirement"`; use `subsystem_id`/`subsystem_ids` to distinguish system-level rows from subsystem-level rows.

Story and stakeholder filters deliberately exclude generated `interface_requirement` rows because interface contracts have no direct story link. If the implementation needs interface context, collect the subsystem IDs from the story-linked requirements and make a second `requirement_items_list` call with `kind: "interface_requirement"` and those `subsystem_ids`, or call `interface_contracts_list`. Generated interface rows are read-only views; update their underlying contracts with `interface_contracts_patch`.

These list calls discover requirements already propagated from a story. Generating them is normally done on the website. When the user explicitly requests generation through MCP, call `projects_propagate_stories` with the selected story UUIDs in `chosen_story_ids` and `project_id`. It uses AI, spends credits, and saves proposals for review; generation does not itself accept them (see "Saved Suggestions").

If no requirements are available, default to asking the user to generate them on the Entalpa website unless they requested MCP generation. Do not fabricate unlinked requirements to fill the gap.

## Find What Changed (Snapshots & Diff)

To implement "only what's new" after the user extends a project: call `projects_list_snapshots` to find a baseline snapshot, then `projects_diff` with `base: <snapshot UUID>` (and `compare` defaulting to `current`). The result groups stories, requirements, and interface contracts into `added` / `removed` / `modified` / `unchanged` buckets with human-readable IDs. Use it to identify work, then discover and confirm the current entities before writing implementation feedback to their UUIDs.

When the task calls for saving a named baseline, use `create_project_snapshot` with `{project_id, snapshot: {name, description?}}` and retain its returned `snapshot_id`. Creating a snapshot is a write, not a prerequisite for reading an existing diff.

You can also narrow `requirement_items_list` server-side instead of fetching everything and filtering client-side. Filter by `story_ids`/`stakeholder_ids`/`subsystem_ids` (UUIDs from earlier reads), by `kind` (`requirement` vs `interface_requirement`), by `flags`, or by a `content_key` (optionally with `content_contains`), e.g. `{content_key: "priority", content_contains: "must"}`. Status is the `lifecycle` field, not a content key, and no list tool filters on it: filter the returned items yourself.

A requirement appears as `modified` in `projects_diff` when only its evidence keys (`code_reference`, `tests`) changed, including through your own writes. Check `changed_fields` before treating it as new work. `lifecycle` changes are not part of the diff.

## Update Project Metadata

- Prefer `projects_patch` for partial project metadata edits.
- Use `projects_update` only when replacing the full project object intentionally. Before `projects_update`, call `projects_get` and include every field that should be preserved.
- Use `projects_undo` and `projects_redo` only when the user asks to revert or replay Entalpa project changes. Confirm the exact project ID and verify `can_undo` or `can_redo` before calling.

## Create Requirements

Use `requirements_create` with:

- `project_id`
- `requirement.content.requirement` (required; `statement` is still accepted as an older name)
- `requirement.content.acceptance`
- `requirement.content.rationale`
- `requirement.content.risk`
- `requirement.content.source`
- `requirement.source_story_ids` when known
- `requirement.flags`, `lock`, or `from_description` only when the user intent or existing project pattern calls for them

Prefer server-generated content IDs unless the project already uses a clear naming convention.

## Update Requirements

- Prefer `requirements_patch` for normal requirement edits.
- Use `requirements_update` only when replacing the full requirement object intentionally. It resets every omitted field among `source_story_ids`, `source_requirement_ids`, `flags`, `lock`, `from_description` and `subsystem_id`. A missing `subsystem_id` turns a subsystem requirement into a system-level one, and a missing `lock` unlocks a locked requirement. An omitted `lifecycle` stays as it was, unless the `content` you send carries `implementation_status` with a recognised value.
- Before `requirements_update`, call `requirements_get` and include every field that should be preserved, including `source_story_ids`, `source_requirement_ids`, `flags`, `lock`, `from_description`, `subsystem_id`, and all existing `content` fields.
- For a locked requirement (`lock: true`), follow "Locked Requirements" in `SKILL.md`.
- The `content` object itself is the exception: whatever `content` you send in `requirements_patch` or `requirements_update` is shallow-merged with the requirement's existing `content` server-side. A patch of `{"lifecycle": "implemented", "content": {"tests": ["…"]}}` does not require re-fetching the requirement first to preserve `requirement`, `acceptance`, etc. — see `references/implementation-feedback.md`.
- Re-read the updated requirement when the result needs confirmation.

## Related Objects

- Use `stories_create` or `stories_update` only when the user asks to add or change stories, or when requirement creation depends on a missing story and the user approves creating it.
- Use `stakeholders_create`, `stakeholders_update`, `subsystems_create`, `subsystems_update`, or interface-contract write tools only when the task explicitly touches those objects.
- Before `subsystems_update`, call `subsystems_get` and include every existing subsystem field that should be preserved.
- Prefer `interface_contracts_patch` for interface-contract edits. Before `interface_contracts_update`, call `interface_contracts_get` and include every field that should be preserved, including `content`, `flags`, and `lock`.

## Saved Suggestions

`projects_generate`, `projects_analyze`, `projects_audit_backlog` and `projects_propagate_stories` use AI and spend credits; run them only when the user asks. Besides returning their proposal, they save it as a batch of suggestions, and the website's review dialogs show the same batch.

1. `suggestions_list` with `project_id` returns pending batches, newest first. Filter with `operation` (`analyze`, `generate`, `audit_backlog`, `propagate_stories`) and `status`. Each item proposes creating, changing or deleting one requirement or story, with the proposed values in `changes`.
2. Review the items with the user.
3. Apply the accepted ones with `suggestions_accept`:
   - pass `items: [{"id": <item id>}]`;
   - `fields` limits an item to some of its keys, and `values` substitutes your own value for a key;
   - everything accepted in one call is a single undo step.
4. Decline the rest with `suggestions_reject` and their `ids`.

`suggestions_accept` is destructive: an item can delete a requirement or story. Some items come back unapplied:
- **`stale`:** the target changed since the run. Re-read the target and ask the user rather than passing `force: true`. Leave stale items out of the next call: sending one again without `force` fails the whole call with a 409.
- **`blocked`:** the item would change or delete a locked requirement, or delete a story that a reviewed requirement depends on.

Do not recreate accepted items with `requirements_create` or `requirements_patch`. The saved suggestions would stay pending, and accepting a creation later would create it a second time. A newer run of the same tool can also replace the pending suggestions of an older one.

## Suspect Links

When a story is edited after requirements were written from it, those requirements are flagged. Their `suspect_story_ids` lists the stories that changed, and the story's `outdated_requirement_ids` lists the requirements.

- `requirements_list` with `story_ids` and `suspect_only: true` returns just the flagged requirements of those stories. `requirement_items_list` does not include `suspect_story_ids`.
- Before implementing a flagged requirement, compare it with the story as it reads now, and tell the user. There are three ways to settle it:
  - rewrite the requirement, with the user's confirmation if it is locked;
  - re-propagate the story with `projects_propagate_stories`, which spends credits;
  - if the requirement still holds, clear the flag with `requirements_confirm_sources`, which uses no AI and no credits.

## Open Questions

Open questions are decisions the spec has not settled yet.

- **Read them first.** Before implementing a story, call `open_questions_list` with its `story_id`. An `open` question on the behavior you are about to build means the requirement may change; ask the user rather than guessing.
- **An `answered` question that has not been converted** (no `resulting_story_id`) is a decision the backlog does not contain yet. Mention it.
- **Recording an answer:** `open_questions_answer` does that.
- **Converting an answer:** `open_questions_convert_to_story` writes it into the backlog, usually by revising the story it was asked about.
  - When `content` is omitted, it drafts the text with AI, which spends credits, even with `dry_run`.
  - Convert only when the user asks.

## Final Response Pattern

End with:

- Project name and ID.
- Created or updated requirement IDs.
- Source story IDs linked to each requirement.
- Assumptions or missing context.
- Any destructive actions performed, if any.
