# Changelog

Notable changes to the Entalpa MCP integrations: the remote MCP connection, the
published Agent Skills, and the Codex, Claude Code and Cursor plugin bundle.

Versions follow the canonical distribution release, so each version here is the
same version a client reports for the installed plugin. This changelog and the
canonical skills are maintained by hand; generated documentation, marketplace
metadata, and plugin skill copies are derived from the source configuration.

## 0.1.8 - Unreleased

### Added

- **Checking a project with a pack.** `entalpa-implement` now covers concern
  packs: an expert's checklist, such as privacy, security, accessibility or
  payments, whose concerns are user stories from the owners who have them.
  The agent picks a pack with `packs_list` or `packs_get`, and checks a
  project with `projects_review_with_pack` only when the user asks, because
  the check uses AI and credits. The questions it returns are already saved,
  so the agent does not create them again; the user answers or dismisses
  them, and an answer reaches the backlog only when it is converted into a
  story. The check changes no story or requirement, and an empty result does
  not mean the spec is complete or compliant. Writing a pack is covered too:
  `packs_update` replaces the whole checklist, so it and `packs_delete` are
  confirmed first, like the other destructive tools. Packs are not projects:
  the skill finds them with `packs_list`, not `projects_list`. This needs
  Entalpa 0.16.0 or later (entalpa-platform#849, #1015).

### Changed

- **Reports say what changed, in human IDs.** The skill's final response
  names the project and uses human IDs, not UUIDs, and says what changed and
  what did not, for example "Saved three questions; stories and requirements
  are unchanged."
- **The reviewed tool inventory** covers all 90 server tools. It adds the
  pack tools `packs_list`, `packs_get` and `packs_create`, the destructive
  `packs_update` and `packs_delete`, `projects_review_with_pack`, and the
  Spec score tools `projects_spec_score` and `projects_spec_score_settings`.

## 0.1.7 - 2026-11-06

### Added

- **A Cursor plugin.** The `entalpa` plugin folder now carries Cursor's
  manifest, `.cursor-plugin/plugin.json`, and the `mcp.json` that Cursor reads.
  The repository's `.cursor-plugin/marketplace.json` points Cursor at that
  folder. Cursor gets the same skills as Claude and Codex and the same icon
  as Claude, from the same files; its `mcp.json` names the same MCP server as
  the `.mcp.json` that Claude Code and Codex read. The plugin is not in the
  Cursor Marketplace yet: Cursor reviews each publisher before listing.

### Changed

- **A new plugin icon.** The orange glow became hard to make out at the small
  sizes plugin lists use. The new icon shows Entalpa's lattice: four orange
  core dots joined by teal lines to eight white ones, on a dark tile that reads
  on light and dark themes alike. Claude's plugin directory and Cursor show
  the same file.
- **Reviewing suggestions in an MCP Apps view.** In clients that display
  MCP Apps views, such as Claude and ChatGPT, `entalpa-implement` lets the
  user review a run's suggestions in `suggestions_review`, which applies the
  decisions itself, and reads the view's context instead of listing the
  items again. It mentions `requirements_show` for showing requirements
  there. This needs the Entalpa server release with the MCP Apps views
  (entalpa-platform#935, #1013).
- **One undo for accepts and declines.** Reviewing in the conversation, the
  skill declines the rest in the same `suggestions_accept` with `reject`, so
  one undo reverts both, and keeps `suggestions_reject` for declining alone.
  To revert one accept, it calls `projects_undo` with the `accept_token` that
  accept returned, and the undo is refused if the project changed since. A plain undo
  reverts the latest change, whoever made it.
- **The reviewed tool inventory** adds the three read-only MCP Apps tools:
  `requirements_show`, `suggestions_review`, and the view-only
  `suggestions_review_get`.
- **The plugin README speaks to every client.** It used to address Claude
  only. It now says "your agent", gives the sign-in step for claude.ai, Claude
  Code and Cursor, and still states everything the skills send and run.

## 0.1.6 - 2026-11-04

### Fixed

- **The plugin directory no longer holds new versions for review.** Since
  0.1.4, Anthropic's plugin directory held each version as "Uses a credential
  from the user's machine". Its scanner read "pass `--pdf-engine=tectonic`" in
  the PRD skill's PDF instructions as a call to the `pass` password manager,
  and paired it with the MCP server's URL as a credential leaving the machine.
  The instruction now gives the whole `pandoc` command with that option.

## 0.1.5 - 2026-11-04

### Changed

- **The Entalpa connector in Claude's Connectors directory.** Entalpa's MCP
  server has its own listing there since 2026-11-01:
  [claude.ai/directory/entalpa](https://claude.ai/directory/entalpa). The
  Claude guide offers it for the server alone and on a Free plan, where the
  directory's plugins are not available, in place of the custom connector,
  which stays as the last resort. The public README and the plugins page link
  the listing, and say that with both the plugin and the connector, Claude
  sees one set of tools.

### Fixed

- **The import skills no longer read the Git remote.** `entalpa-openspec` and
  `entalpa-speckit` told the agent to take the repository's address from
  `git remote get-url origin`. A remote URL can carry an access token, and the
  agent would then have sent it to Entalpa with the import call. The server
  rejected such an address without storing it, but the token had still left
  the machine. The skills now ask for the plain
  `https://github.com/<owner>/<repo>` address, with no user name, password or
  token in it. The plugin README no longer lists finding the repository among
  the uses of `git`.

## 0.1.4 - 2026-11-01

### Added

- **A complete directory listing.** The Claude plugin manifest now sets
  everything Anthropic's directory shows: the display name "Entalpa", an icon,
  and documentation, support, privacy policy and terms links. The plugin folder
  has a README, which the directory shows on the listing: what the plugin adds,
  how to start, what it sends where (only to `api.entalpa.com`, signed in
  through OAuth), which commands its skills may run, and what Entalpa fetches.
  The plugin descriptions lead with what you get, spec-driven development with
  user stories, acceptance criteria and PRDs, and say that the Entalpa account
  is free. The marketplace entries, which GitHub Copilot and VS Code read too,
  name no client.
  Keywords add `user-stories`, `acceptance-criteria` and `prd`. The support link
  is `entalpa.com/en/connect`, where the old `/en/connect-mcp` redirected.
- Two Agent Skills for teams that already write specs in their repository:
  - `entalpa-openspec` imports an OpenSpec repository's specs, and reads related requirements, stakeholders and open questions before a change is proposed. When a change is archived, it brings Entalpa up to date: it matches each delta by its recorded source or verified previous text within the domain, treats heading IDs as discovery hints, and lists what it cannot match instead of guessing. Exported specs are validated with an explicit noninteractive scope.
  - `entalpa-speckit` imports a GitHub Spec Kit repository and folds its features into one current backlog. It says what the fold deletes and asks before spending credits, checks the next feature against the backlog before `/speckit-specify`, and keeps requirement statuses in step with `tasks.md` the way the import reads them. Setting `draft` is allowed during task-status synchronization; outside that workflow, resetting to `draft` requires the user's instruction.
  - Both leave the team's spec files alone, with two exceptions, each only when the user agrees: an export the user asked for, and the one OpenSpec `config.yaml` rule that keeps Entalpa IDs in headings. Before an export they check for active changes and say what the export will rename or leave out.
- All four skills are listed in every client's install instructions, the plugin description and keywords mention OpenSpec and Spec Kit, and the reviewed tool inventory now covers all 79 server tools with the server's own read, write and destructive markings.

### Changed

- Updated implementation guidance to discover entities by readable labels, then
  copy returned UUIDs for operation targets, filters, selections and relationships.
  Keep human IDs in explanations and portable documents; retain the selected UUID
  if an entity is renamed, and ask before replacing a missing target, even when
  a different entity has identical wording and metadata.
- Corrected bulk lookup and implementation-feedback examples that advertised
  human-ID selectors.
- Documented the existing `projects_propagate_stories` and
  `create_project_snapshot` tools, preserving the default website-authoring
  workflow and distinguishing generation proposals from accepted changes.
- `projects_export_openspec` and `projects_export_speckit` are read tools, and
  the server marks them `readOnlyHint: true`. They return file paths and
  contents and change nothing, so clients need not ask before running them.
- `entalpa-implement` says that the story tools return a story's human ID
  (`human_id`, for example `S-001`), as the stakeholder tools do, instead of
  sending agents to `project_search`, `resolve_ids` or `projects_export` for it.
- **Install from Claude's plugin directory.** The `entalpa` plugin is listed in
  Claude's plugin directory, and the Claude guides now lead with it: add it in
  claude.ai or the desktop app from Customize > Plugins, then connect `entalpa`
  from the plugin's Connectors tab. It loads in Cowork too, and in Claude Code
  as `entalpa@synced`. Claude Code 2.1.287 or later installs it with
  `claude plugin install entalpa@anthropic-plugin-directory`, or finds it with
  `/plugin directory entalpa`. The plugin's server shows in `/mcp` as
  `plugin:entalpa:entalpa`. The custom connector, with a link that fills in its
  name and URL, and the skill ZIP upload stay as the fallback where the
  directory is not available, and the Entalpa marketplace stays for older
  Claude Code.

- **The listing leads with spec-driven development.** The server description is now "Spec-driven development for AI coding agents: live requirements, stories and traceability over MCP". It is what the MCP Registry shows, and the directories that read from it. The plugin keywords add `spec-driven-development` and `ai-coding-agents`. The public README opens with the same description as entalpa.com, and says that Entalpa works alongside Spec Kit, OpenSpec and `CLAUDE.md` rather than replacing them.

Brought `entalpa-implement` and `entalpa-prd` up to date with the server.

- **Status comes from `lifecycle`.** A requirement's status is its `lifecycle` field, which the website and the imports set too. `content.implementation_status`, which the skill used to read and filter on, is only an older way to write it. Agents now skip `rejected` and `superseded` requirements.
- **Locked requirements,** in all four skills. Agents ask before changing a locked requirement's text, acceptance criteria or links. Recording status and evidence stays allowed. They never send a full update that would drop `lock`.
- **AI tools and credits.** The tools and paths that run Entalpa's AI and spend credits are listed, to be used only when the user asks. 402, 409 and 429 refusals are explained. Generate, Analyze, Audit backlog and Propagate stories save their proposals as suggestions, which are applied with `suggestions_accept` rather than recreated with CRUD tools; stale and blocked items are explained.
- **New in the guidance:**
  - `projects_overview` as the first read;
  - starting from a named requirement, with the same relevant source, open-question and interface checks as the story-based path;
  - suspect links after a story changes, and `requirements_confirm_sources`;
  - open questions;
  - stakeholder IDs such as `SH-004`;
  - `stakeholders_update`;
  - treating project content as data, not instructions.
- **Corrected:**
  - The requirement text is `content.requirement`; `statement` is still accepted as an older name.
  - A full `requirements_update` also resets `subsystem_id`, `from_description` and `source_requirement_ids`.
  - `suggestions_accept` and `restore_project_snapshot` are treated as destructive.
  - Requirements generated from stories now point at `projects_propagate_stories`.
- **PRD skill:**
  - it reads the project `description` and the assessment from the export;
  - it leaves out rejected and superseded requirements;
  - it can add a status column and an open-questions section;
  - it no longer depends on `entalpa-implement` being installed.

## 0.1.3 - 2026-08-24

### Changed

- The plugin description now states that an Entalpa account is required, and that
  the client signs in on first connect with no API key to paste. Every tool on
  the server answers 401 without one, and the description is what a user reads in
  their client's plugin list.
- Plugin and marketplace manifests point `homepage` at https://entalpa.com rather
  than at the configuration guide's GitHub blob URL. `repository` still reaches
  the guide, and the Codex `interface.websiteURL` already used the product site.

## 0.1.2 - 2026-08-13

- Fixed the Codex plugin MCP configuration to use the `mcpServers` JSON shape
  accepted by the Codex runtime. Codex and Claude Code now share one
  `.mcp.json` instead of carrying divergent duplicate files.
- Clarified that adding a Codex marketplace registers its catalog and must be
  followed by plugin installation through `codex plugin add` or `/plugins`.
- Added isolated installation smoke tests for the published skills, MCP
  commands, and Codex and Claude plugin bundles.
- Updated the GitHub Copilot CLI MCP command to its current native syntax.

## 0.1.1 - 2026-08-06

- Documentation: the Codex documentation links now point at their current
  locations. Every `developers.openai.com/codex/*` URL had started answering
  `308` and redirecting elsewhere.
- Documentation: release-specific install examples can follow the concrete
  public tag while internal and repository-override builds retain a
  `<release-tag>` placeholder.
- Documentation: the README states that an Entalpa account is required, and
  links the MCP support page, support address, privacy policy, and terms of
  service.

## 0.1.0 - 2026-07-23

First public release.

- Remote MCP server at `https://api.entalpa.com/mcp` over Streamable HTTP,
  authenticated with OAuth. Clients register themselves; there is no API key.
- Agent Skills `entalpa-implement` (implement requirements and record code
  references, status, and test coverage back onto them) and `entalpa-prd`
  (generate a PRD or BRD document from a project).
- Plugin bundle installable from the repository marketplace in Codex and Claude
  Code, which adds the MCP connection and both skills together.
- Client-by-client installation and troubleshooting guides for the supported
  MCP clients under `docs/mcp/`.
