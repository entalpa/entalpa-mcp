---
name: entalpa-prd
description: Use this skill to generate a human-readable PRD/BRD document artefact from an Entalpa project over its MCP server — a stakeholder-facing spec (business-requirements narrative, per-subsystem functional and non-functional requirements with stable codes, data & storage and Definition-of-Done tables, and story/requirement traceability) exported as Markdown and, optionally, PDF. Covers the whole project or a selected subset of subsystems/stories. It reads project data and writes a document; it does not modify the project unless the user explicitly asks.
license: MIT
---

# Entalpa PRD

Entalpa is a requirements-engineering platform where humans author project context (project idea, stakeholders, stories) and generate system- and subsystem-level requirements on the website. This skill turns that structured spec into a **human-readable PRD/BRD document** — the kind of single document a product owner hands to stakeholders, compliance, or a vendor for an RFP.

The Entalpa exports that already exist (portable JSON, requirements JSON/CSV/Markdown, ReqIF XML) are **data-interchange** formats. This skill instead produces a **presentation-ready narrative document**: a business-requirements section written in prose, followed by per-subsystem specs with coded requirement lists and structured tables.

**This skill is read-only.** You read the project over MCP and produce a document file. Do not create, patch, or delete any Entalpa entity while generating a PRD. Only touch write tools if the user explicitly asks you to fix the underlying data first, in which case follow the `entalpa-implement` skill's read-before-write discipline.

## Grounding Rule (do not fabricate)

Every statement, requirement, acceptance criterion, and constraint in the document must come from the project's stored data. The prose sections may be **rephrased and organized** for readability, but must not invent requirements, numbers, vendors, or decisions that aren't in the project. When a section has no data, say so plainly ("No non-functional requirements are recorded for this subsystem yet") rather than filling the gap. Never redact or paraphrase away a requirement to make the document look more complete.

## Core Workflow

1. **Authenticate & select the project.** Call `users_get_me`, then `projects_list`/`projects_get`. If more than one project could match, ask the user which one before generating anything.
2. **Determine scope.** Whole project, one or more subsystems, or a chosen set of stories/requirements. If the user didn't say, default to the whole project (see `references/customization.md` for how to infer and confirm scope).
3. **Gather the data.** Call `projects_export` once for the selected project; its portable payload contains the project, subsystems, stakeholders, stories, requirements, interface contracts, and their relationships expressed with human-readable IDs. Call `projects_get_assessment` separately for the quality/readiness warning. Filter the export locally to the selected subsystems, stories, or requirements while retaining the linked entities needed for traceability. Use targeted list/get tools only to resolve an ambiguous scope before export or refresh a specifically requested entity. Reuse exported `human_id` values (for example `Req-012`, `S-3`, `Sub-002`) as stable document codes.
4. **Offer customization.** Infer sensible defaults from what the project actually contains and confirm them in one concise question before writing the document — see `references/customization.md`.
5. **Assemble the document** following `references/document-structure.md`: title + summary, Part I business-requirements narrative, one section per subsystem (purpose & boundaries, coded functional/non-functional requirements, data & storage table, Definition-of-Done table), and a traceability section.
6. **Render output.** Write the Markdown file, then convert to PDF if requested — see `references/output-formats.md`. Degrade gracefully (deliver Markdown) if no PDF toolchain is available.
7. **Summarize.** Report the project name/ID, the scope covered, the file(s) written, and anything thin or missing in the source data (e.g. "Billing subsystem has 2 requirements and no acceptance criteria — the DoD table is sparse").

## Customization (ask, with smart defaults)

Users should be able to shape the document, but shouldn't have to answer a long questionnaire. Inspect the project first, propose the choices that fit its contents, and ask a single confirm-or-adjust question. For example: with a project that has three subsystems, populated `rationale`/`risk`, and interface contracts, propose a per-subsystem BRD in the project's apparent language, with rationale and risk columns, an interfaces section, and PDF output — then let the user change scope, sections, language, or format. Full inference rules and the phrasing pattern are in `references/customization.md`.

## Reference Loading

- Read `references/document-structure.md` before assembling the document — it defines the section order, the requirement→section/table mapping, coding and grouping rules, and how to handle missing fields.
- Read `references/customization.md` before step 4 — it lists the customization dimensions, the defaults to infer from project contents, and how to ask in one question.
- Read `references/output-formats.md` before rendering — Markdown conventions, PDF conversion options, file naming, and graceful fallback.

## Non-Destructive Guarantee

Generating a PRD never calls a write or destructive tool. If the source data is wrong or incomplete, report it in the summary and suggest fixing it on the Entalpa website or via the `entalpa-implement` skill — do not silently edit the project to make the document look better.
