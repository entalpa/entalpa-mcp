# Entalpa Plugins and Registries

<!-- Generated from Entalpa's canonical integration source. -->

This page covers bundled plugin installation and discovery/registry artifacts for the Entalpa MCP server.

## Plugin Bundle

The plugin bundle lives at `plugins/entalpa` and includes:

- Codex manifest: `plugins/entalpa/.codex-plugin/plugin.json`
- Claude Code manifest: `plugins/entalpa/.claude-plugin/plugin.json`
- Shared Codex and Claude Code MCP config: `plugins/entalpa/.mcp.json`
- Skill: `plugins/entalpa/skills/entalpa-implement/SKILL.md`
- Skill: `plugins/entalpa/skills/entalpa-prd/SKILL.md`
- Skill: `plugins/entalpa/skills/entalpa-openspec/SKILL.md`
- Skill: `plugins/entalpa/skills/entalpa-speckit/SKILL.md`

The plugin installs the Entalpa MCP server and all configured skills together: `entalpa-implement`, `entalpa-prd`, `entalpa-openspec`, `entalpa-speckit`.

The unpinned marketplace commands below read `entalpa/entalpa-mcp`'s default branch. Use the pinned release commands in [release-and-versioning.md](release-and-versioning.md) when you need a reproducible version.

## Claude Directory

The `entalpa` plugin is listed in Claude's plugin directory. In claude.ai or the Claude desktop app, open [Customize > Plugins](https://claude.ai/customize/plugins), search for Entalpa on the **Discover** tab, and select **Add**; then connect `entalpa` from the plugin's **Connectors** tab. The plugin is saved to the Claude account, so Cowork loads it too, and Claude Code 2.1.273 or later loads it as `entalpa@synced` in sessions signed in with that account.

Claude Code 2.1.287 or later also installs it straight from the directory, which it carries as the built-in `anthropic-plugin-directory` marketplace (`/plugin directory entalpa` finds it from a session):

```bash
claude plugin install entalpa@anthropic-plugin-directory
```

The directory reads the listing from `plugins/entalpa/.claude-plugin/plugin.json` and the plugin README of the published repository, so changing the listing takes publishing a new version.

## Codex

Add the repository marketplace:

```bash
codex plugin marketplace add entalpa/entalpa-mcp --sparse .agents/plugins --sparse plugins
codex plugin add entalpa@entalpa-plugins
```

The first command registers the catalog; the second installs and enables `entalpa`. As a UI alternative to the second command, open `/plugins` in Codex, choose the Entalpa Plugins marketplace, and install the plugin there.

## Claude Code

On Claude Code older than 2.1.287, or where an organization blocks the directory, add the repository marketplace:

```bash
claude plugin marketplace add entalpa/entalpa-mcp --sparse .claude-plugin plugins
```

Install the plugin:

```bash
claude plugin install entalpa@entalpa-plugins
```

After installing or enabling a plugin in an active Claude Code session, restart Claude Code or run `/reload-plugins` before verifying MCP tools. The plugin's server appears in `/mcp` as `plugin:entalpa:entalpa`.

## Discovery

Use native installers and the plugin marketplaces above. Registry and directory listings are documented here only after publication and verification.

## Sources

- [Codex Plugins](https://learn.chatgpt.com/docs/plugins)
- [Build Codex plugins](https://developers.openai.com/plugins/build/plugins)
- [Plugins in Claude](https://claude.com/docs/plugins/overview)
- [Claude Code plugins synced from claude.ai](https://code.claude.com/docs/en/plugins/loading#synced-plugins)
- [Claude Code plugin marketplaces](https://code.claude.com/docs/en/plugin-marketplaces)
- [Claude Code plugins reference](https://code.claude.com/docs/en/plugins-reference)
- [MCP Registry](https://modelcontextprotocol.io/registry/about)
- [Configure MCP servers for GitHub Copilot coding agent](https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/configure-mcp-servers)
- [Smithery publish MCP servers](https://smithery.ai/docs/build/publish)
- [Glama MCP directory](https://glama.ai/)
- [mcp.so MCP directory](https://mcp.so/)
