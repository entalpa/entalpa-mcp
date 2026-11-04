# Entalpa

<!-- Generated from Entalpa's canonical integration source. -->

Spec-driven development in Claude: keep user stories, requirements and acceptance criteria in Entalpa, draft PRDs from them, and have Claude implement against that spec, linking the code back to each requirement it covers. Imports and exports OpenSpec and GitHub Spec Kit. Requires a free Entalpa account.

## What the plugin adds

- **The `entalpa` connector**: Entalpa's remote MCP server at `https://api.entalpa.com/mcp`. Through it, Claude reads and writes the projects your Entalpa account can see: stakeholders, user stories, requirements with their acceptance criteria, open questions, and the links between them.
- **Skills** that tell Claude how to work with that spec:
  - `entalpa-implement`: Implement Entalpa requirements with traceability.
  - `entalpa-prd`: Generate grounded PRD and BRD documents.
  - `entalpa-openspec`: Keep OpenSpec specs and Entalpa in step.
  - `entalpa-speckit`: Fold Spec Kit features into one current spec.

## How to use it

1. Create a free Entalpa account at [entalpa.com](https://entalpa.com).
2. Connect to Entalpa. In claude.ai or the Claude desktop app, open the plugin's **Connectors** tab and connect `entalpa`. In Claude Code, run `/mcp`, select `plugin:entalpa:entalpa`, and sign in. Entalpa's sign-in opens in your browser; there is no API key to paste.
3. Ask Claude for what you need, for example:
   - "Use Entalpa to inspect my project, identify missing requirements, and preserve traceability."
   - "Use Entalpa to implement the current requirements and record implementation evidence."
   - "Use Entalpa to generate a grounded PRD or BRD from the current project."
   - "Use Entalpa to bring this repository's OpenSpec or Spec Kit specs into one current spec."

## Data and privacy

The plugin has no hooks, scripts or local servers, and stores nothing itself. Its skills are instructions for Claude, and its only connection is the `entalpa` MCP server at `https://api.entalpa.com/mcp`, over HTTPS and signed in with your Entalpa account through OAuth.

- **What Claude sends to Entalpa:** the reads and changes you ask for, in the projects your account can see. While implementing, the skills record on each requirement its status, where in the code it is implemented and which tests cover it: file paths, test names and a short note, not the code itself. `entalpa-openspec` also copies the requirement text of an archived OpenSpec change into the project, and `entalpa-speckit` sets requirement statuses from the ticks in `tasks.md`.
- **Commands the skills may run** where Claude has a terminal, with your usual approval: `git`, for an export you ask for, to put the written spec files on a new branch; the `openspec` CLI, to read and validate OpenSpec specs; and a converter such as `pandoc` when you ask for a PRD as a PDF.
- **What Entalpa fetches:** importing an OpenSpec or Spec Kit repository has Entalpa's server read that public GitHub repository.

Entalpa stores your projects. How it handles them, including what a connected client may do and which AI providers Entalpa's own AI features use, is in the [privacy policy](https://entalpa.com/en/privacy-policy). Use is subject to the [terms of service](https://entalpa.com/en/terms-of-service).

## Support

- Setup guides and help, for Claude and other clients: https://entalpa.com/en/connect
- Email: contact@entalpa.com
