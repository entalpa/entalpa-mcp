# PRD/BRD Document Structure

Use this reference when assembling the document. It defines the section order, how each part maps to Entalpa data, coding and grouping rules, and how to handle missing fields. The target shape is a single BRD/ТЗ-style document: a business-requirements narrative followed by per-subsystem specs with coded requirement lists and tables.

## Where the content comes from

| Document part | Entalpa source |
|---|---|
| Title + one-line summary | `projects_export`: project `title`; a one-sentence summary distilled from `design_description` |
| Part I business-requirements narrative | `projects_export`: `design_description`, stakeholder descriptions and story content |
| Per-section grouping | Exported `subsystems` (`human_id`, `name`, `description`). No subsystems → one "System" section for the whole project |
| Purpose & boundaries | Subsystem `description`; "what it does NOT do" from any explicit non-goals in stories/requirements — omit if absent, do not invent |
| Coded requirement list | Exported `requirements`: `content.requirement`, keyed by top-level `human_id` (the same value as `content.id`) |
| Functional vs non-functional / constraints | `content.category` / `content.component` when present; otherwise list all under "Requirements" |
| Data & storage table | Requirement `content` fields describing data/storage where the project records them; otherwise omit the table |
| Definition of Done / acceptance table | Requirement `content.acceptance` |
| Rationale / risk columns | Requirement `content.rationale`, `content.risk` (include only if populated and the user kept them) |
| Traceability / cross-links | Exported requirement `source_story_ids` / `source_requirement_ids` and exported interface contracts; all relationship IDs are human-readable IDs |

## Section order

1. **Title & summary** — project title as `# H1`, then a 1–2 sentence plain-language summary and a short table of contents.
2. **Part I — Business requirements** (prose, LLM-written but grounded):
   - *What we want to do* and *why* — the problem today, drawn from `design_description` and stakeholder needs.
   - *Who it's for* — stakeholders and the outcomes each cares about.
   - *What we propose* / *What we gain* — the intended solution and its value, only as far as the project data supports.
   - *Principles / constraints* — cross-cutting rules if the project records them.
3. **Per-subsystem sections** (repeat for each subsystem in scope; a single section if the project isn't decomposed):
   - `## <Subsystem name>` with a short purpose line and, if recorded, a "does / does not do" boundary list.
   - **Requirements** — a coded list. Each item: `**<human_id>** — <content.requirement>`, optionally followed by rationale/risk sub-lines. Split into "Functional" and "Non-functional / constraints" only when categories distinguish them.
   - **Data & storage** — a table only if the project records data/storage details; otherwise skip.
   - **Definition of Done** — a table of `<human_id>` → acceptance criteria for every requirement that has `acceptance`.
4. **Traceability** — a compact table or list mapping requirements to their source stories (`source_story_ids`) and, for subsystem-level requirements, their parent system requirements (`source_requirement_ids`). The portable export expresses these links with human-readable IDs. Include an **Interfaces** subsection listing exported interface contracts (`source_subsystem_id` → `target_subsystem_id`, `interface_type`, `description_payload`) when any exist.
5. **Appendix (optional)** — stakeholder list, story list, or a glossary if the user asked for them.

## Coding & grouping rules

- Use each requirement's existing `human_id` (e.g. `Req-012`) as its stable code in the document. Do **not** renumber into `F-1`/`C-1` unless the user asks for a re-coded scheme — the project's human ids are the canonical references and preserve traceability.
- Group by subsystem first, then by category/component within a subsystem when those fields exist.
- List requirements in a stable order (by `human_id`) so regenerating the document produces a stable diff.

## Handling missing or optional fields

- A requirement with no `acceptance` still appears in the requirements list; it just has no Definition-of-Done row. Note sparse coverage in the summary rather than inventing criteria.
- If a subsystem has no requirements in scope, include the section header with a one-line "No requirements recorded yet."
- If the project has no subsystems, no stakeholders, or no stories, omit those sections/columns gracefully instead of leaving empty scaffolding.
- Never drop a requirement to tidy the layout — completeness beats neatness for a spec.

## Faithfulness

Prose may reorganize and summarize, but every requirement, acceptance criterion, constraint, number, and name must trace back to project data. When you summarize a `design_description`, keep its claims; do not add market claims, vendors, costs, or decisions that aren't there.
