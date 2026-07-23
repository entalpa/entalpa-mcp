# Output Formats: Markdown and PDF

The document is authored as **Markdown** and optionally rendered to **PDF**. Markdown is always the source of truth; PDF is a rendering of it.

## Markdown conventions

- One `# H1` title; `##` per top-level section (Part I, each subsystem, Traceability); `###` for sub-parts.
- Use Markdown tables for Definition-of-Done, data & storage, and traceability so they survive PDF conversion.
- Use `**<human_id>**` as the bolded code prefix for each requirement so codes stay scannable in both Markdown and PDF.
- Keep the file self-contained (no external image dependencies) so conversion is reliable.

## File naming and location

- Write to the current working directory (or a path the user specifies).
- Name the file from the project title and scope, slugified: `<project-slug>-prd.md` for a whole-project export, or `<project-slug>-<subsystem-slug>-prd.md` for a scoped one.
- Write the PDF alongside it with the same base name and a `.pdf` extension.

## PDF conversion

Convert the Markdown to PDF with whatever is available in the environment, in this order of preference:

1. **Pandoc** (best fidelity for tables): `pandoc <file>.md -o <file>.pdf` (needs a LaTeX engine such as `tectonic`/`xelatex`; pass `--pdf-engine=tectonic` if available).
2. **md-to-pdf** (Node, headless Chromium): when the executable is already installed, run `md-to-pdf <file>.md`.
3. **Headless browser print** — render the Markdown to HTML, then print to PDF.

Check the tool exists before invoking it (for example, `command -v pandoc` or `command -v md-to-pdf`). Do not use `npx md-to-pdf`, because `npx` may download and execute the package implicitly. Ask before installing any missing converter or heavy toolchain.

## Graceful fallback

If no PDF toolchain is available:

- Still deliver the Markdown file — it is the primary artefact.
- Tell the user PDF conversion was skipped and give the exact one-line command they can run locally (e.g. `pandoc <file>.md -o <file>.pdf`).

Do not fail the whole task because PDF rendering isn't possible; a correct Markdown document plus a conversion hint is a successful result.

## Non-Latin scripts

When the document language uses a non-Latin script (e.g. Cyrillic), prefer a Unicode-capable engine (`xelatex`/`tectonic` via Pandoc, or the browser-based paths, which handle Unicode natively). If only a Latin-only engine is available, deliver Markdown and note the limitation rather than producing a PDF with missing glyphs.
