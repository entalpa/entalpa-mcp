# Recording Implementation Feedback

When you implement a requirement's behavior in code, write what you did back onto the requirement so the Entalpa website reflects real progress. Status and evidence are two separate things: status is the requirement's `lifecycle` field, and the evidence goes into a few flat keys in its `content`.

## Status: `lifecycle`

Every requirement has a top-level `lifecycle`, returned by `requirements_list`, `requirements_get` and `requirement_items_list`. It is the one source of truth for where a requirement stands. People set it on the website, and imports set it too; for example, a Spec Kit import takes it from the ticks in `tasks.md`. So read it before you start.

| Value | Meaning | Who sets it |
|---|---|---|
| `draft` | written, not reviewed yet (the default) | anyone |
| `in_review`, `reviewed` | the spec itself is being or has been reviewed | the team |
| `in_progress` | implementation has started | you, when you start |
| `implemented` | the code is in | you, when the change is done |
| `verified` | the tests that cover it pass | you, only after running them |
| `blocked` | work cannot continue | you, with `content.implementation_notes` saying why |
| `rejected`, `superseded` | no longer wanted, or replaced by another requirement | the team; do not implement these |

Set only `in_progress`, `implemented`, `verified` and `blocked`. `draft`, `in_review`, `reviewed`, `rejected` and `superseded` are decisions about the spec, not about the code; leave them to the user unless they ask.

`content.implementation_status` is an older way to write the status. `in_progress`, `implemented`, `verified` and `blocked` written there still update `lifecycle`, and `not_started` is ignored. Write `lifecycle` directly. Never read status from `content.implementation_status`: work done on the website or by an import does not set it.

## Evidence: Flat Keys in `content`

Add these keys to `content`, alongside the descriptive keys (`requirement`, `acceptance`, `rationale`, …). Every value must be a string or a list of strings; the server rejects nested objects and other types:

- `code_reference`: a list of pointers to where the behavior lives. File paths, optionally with line ranges (e.g. `"backend/entalpa/api/routes/stories.py:120-160"`), PR URLs, or commit SHAs.
- `tests`: a list of test identifiers or paths that cover the requirement, e.g. `"backend/entalpa/tests/api/routes/test_stories.py::test_create_story"`.
- `implementation_notes`: a short string for caveats, partial coverage, follow-up work, or why the requirement is `blocked`. Optional.

Do not invent additional structure, such as a nested `implementation` object. Flat keys are schema-valid, and they let you update one field without touching the others.

## One Patch Does Both

`requirements_patch` sets the fields you send and merges the `content` you send into the existing `content` on the server. So one call records status and evidence without re-reading the requirement first:

```python
# requirement_id is the UUID returned by requirements_list/get, or item_id
# from a requirement_items_list entry with kind == "requirement"; not content.id.
await client.call_tool(
    "requirements_patch",
    {
        "project_id": project_id,
        "requirement_id": requirement_id,
        "patch": {
            "lifecycle": "implemented",
            "content": {"code_reference": [path], "tests": [test_id]},
        },
    },
)
```

This changes `lifecycle`, `code_reference` and `tests`, and leaves `requirement`, `acceptance` and every other content key untouched.

**Locked requirements.** Status and evidence updates like this one are fine on a locked requirement (`lock: true`). Anything beyond these keys needs the user's confirmation; see "Locked Requirements" in `SKILL.md`.

**Avoid `requirements_update` here.** A full update replaces the fields it is not given: `flags`, `lock`, `from_description`, `subsystem_id`, `source_story_ids` and `source_requirement_ids` (see `references/tool-workflows.md`).

## Workflow

1. Before implementing, read `lifecycle` on each requirement returned by `requirement_items_list`.
   - Skip anything `implemented` or `verified` unless the user asks you to redo it.
   - Skip anything `rejected` or `superseded`.
2. Set `lifecycle: "in_progress"` when you start, if the work will take more than one step.
3. Implement the change and write or update tests.
4. Patch `lifecycle: "implemented"` with `code_reference` and `tests` in one call.
   - Set `verified` only after the tests pass.
5. If you get partway, set `lifecycle: "blocked"` and say why in `implementation_notes`, rather than leaving stale or misleading state. Partway means, for example, blocked on a missing subsystem requirement or an ambiguous acceptance criterion.
6. In your final summary, list the updated requirements by their human IDs, with their new status and their `code_reference` and `tests`.

## Finding Requirements by Status

The MCP list tools have no status filter. List the requirements in scope and filter on `lifecycle` yourself.
- **Scope:** narrow the list with `requirement_items_list` and `story_ids` or `subsystem_ids`, using UUIDs from earlier reads.
- **Every requirement has a `lifecycle`.** A requirement nobody has touched is `draft`.
- **Evidence keys can be filtered server-side.** `{content_key: "code_reference"}` keeps only the requirements that already carry code references.
