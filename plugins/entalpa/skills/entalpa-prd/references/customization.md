# Customization: Ask Once, With Smart Defaults

The document should be customizable, but the user shouldn't have to fill in a form. **Inspect the project first, infer the choices that fit its contents, then confirm them in a single question** the user can accept or adjust. If the user already stated their preferences (scope, format, language), skip the question and honor them.

## Customization dimensions

- **Scope** — whole project, specific subsystem(s), or specific story/requirement set.
- **Structure** — one section per subsystem, or a single combined "System" section.
- **Included sections/columns** — rationale, risk, data & storage table, traceability, interfaces, appendices (stakeholder/story lists, glossary).
- **Narrative depth** — terse (tables-forward) vs detailed prose in Part I and the per-subsystem intros.
- **Language / locale** — the document's written language.
- **Audience framing** — stakeholder BRD (default), vendor RFP (emphasize constraints, DoD, interfaces), or compliance (emphasize traceability and acceptance).
- **Output format** — Markdown only, or Markdown + PDF (see `references/output-formats.md`).

## Defaults to infer from project contents

Read the complete portable project payload with `projects_export`, call `projects_get_assessment` for its readiness assessment, and choose defaults:

- **Structure** — more than one subsystem → per-subsystem sections; zero or one subsystem → a single combined section.
- **Scope** — default to the whole project; if the user named a subsystem or story, scope to that and offer to widen.
- **Rationale / risk columns** — include only if a meaningful share of requirements actually populate `content.rationale` / `content.risk`; otherwise omit to avoid empty columns.
- **Interfaces section** — include only if the export contains interface contracts.
- **Data & storage table** — include only if requirements record data/storage details.
- **Language** — infer from the project's `title`/`design_description` and requirement text (e.g. a Russian `design_description` → default to a Russian document); fall back to English when mixed or unclear. Always let the user override.
- **Audience** — default to a stakeholder-facing BRD.
- **Format** — default to Markdown plus PDF when a PDF toolchain is likely available; otherwise Markdown, and mention PDF as an option.
- **Thin-data warning** — if `projects_get_assessment` is low or requirements are few / lack acceptance, say so in the confirm message so the user can enrich the project first or proceed knowingly.

## How to ask (one message)

State the inferred plan compactly and invite adjustments in a single question — don't enumerate every dimension as a separate prompt. For example:

> This project has 3 subsystems with rationale and risk filled in and 2 interface contracts, so I'll generate a **per-subsystem BRD in English**, including **rationale + risk** columns, an **interfaces** section, and full **Definition-of-Done** tables, exported as **Markdown + PDF**. Want to change the **scope, sections, language, or format** — or shall I go ahead?

Then:

- If the user accepts (or doesn't object), proceed with the proposed defaults.
- If the user adjusts one dimension, keep the other inferred defaults and regenerate the plan only as needed — don't re-interrogate.
- Only ask a second question if a genuine ambiguity remains (e.g. two projects match the name, or the requested scope is empty).

Keep the interaction proportional: for a quick "just export the whole thing to PDF" request, a one-line confirmation of the inferred plan is enough.
