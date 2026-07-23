# Recording Implementation Feedback

When you implement a requirement's behavior in code, write what you did back onto the requirement so the Entalpa website reflects real progress. There is no dedicated schema for this yet — it is a convention layered onto the free-form `content` object described in `references/entity-model.md`. Follow it consistently so future agents (and humans) can rely on it.

## Convention Keys

Add these keys directly to `content`, alongside the existing descriptive keys (`statement`, `acceptance`, `rationale`, etc.). Every value must be a string or a list of strings — the server rejects nested objects or other types:

- `implementation_status`: one of `not_started`, `in_progress`, `implemented`, `verified`, `blocked`. Use `verified` only once tests for the requirement pass; use `blocked` when you cannot proceed and explain why in `implementation_notes`.
- `code_reference`: a list of pointers to where the behavior lives — file paths (optionally with line ranges, e.g. `"backend/entalpa/api/routes/stories.py:120-160"`), PR URLs, or commit SHAs.
- `tests`: a list of test identifiers or paths that cover the requirement, e.g. `"backend/entalpa/tests/api/routes/test_stories.py::test_create_story"`.
- `implementation_notes`: a short string for caveats, partial coverage, or follow-up work. Optional.

Do not invent additional structure (e.g. a nested `implementation` object) — flat keys are both schema-valid and let you update one field without touching the others (see below).

## Why a Single-Key Patch Is Safe

`requirements_patch` and `requirements_update` both shallow-merge the `content` object you send with the requirement's existing `content` on the server — this happens automatically, including when a project's own LLM jobs regenerate a requirement. So:

```python
await client.call_tool(
    "requirements_patch",
    {
        "project_id": project_id,
        "requirement_id": requirement_id,
        "patch": {"content": {"implementation_status": "implemented", "tests": [test_id]}},
    },
)
```

...updates only `implementation_status` and `tests`, leaving `statement`, `acceptance`, `rationale`, `code_reference`, and every other existing key untouched. You do **not** need to call `requirements_get` first just to preserve content when you're only adding or updating implementation-feedback keys. (You still need `requirements_get` first before a full `requirements_update`, since that call replaces `flags`, `lock`, `source_story_ids`, and `source_requirement_ids` wholesale when they're omitted — see `references/tool-workflows.md`.)

## Workflow

1. Before implementing, check `content.implementation_status` on each requirement returned by `requirement_items_list`. Skip anything already `implemented` or `verified` unless the user asks you to redo it.
2. Implement the change and write or update tests.
3. Patch `implementation_status`, `code_reference`, and `tests` together in one call once the change is in place. Set `implementation_status: "verified"` only after running the tests.
4. If you get partway through (e.g. blocked on a missing subsystem requirement, or an ambiguous acceptance criterion), set `implementation_status: "blocked"` and use `implementation_notes` to say why, rather than leaving stale or misleading state.
5. Mention the updated requirement IDs, their new status, and their `code_reference`/`tests` values in your final summary to the user.

## Quick Filtering

`implementation_status` lives inside `content`, so filter for it server-side with `requirement_items_list` using the generic content filter: `{content_key: "implementation_status"}` keeps only items that have the key set, and adding `content_contains` narrows by value (case-insensitive substring), e.g. `{content_key: "implementation_status", content_contains: "in_progress"}`. You can also scope by `story_ids`/`subsystem_ids` (UUIDs or human ids) and by `flags`. Treat a missing `implementation_status` key the same as `not_started` — note that `content_key` matches only items where the key is present, so "not yet started" requirements are found by their absence from a `content_key: "implementation_status"` result, not by filtering.
