# Entalpa Plugins and Registries

<!-- Generated from Entalpa's canonical integration source. -->

This page covers bundled plugin installation and discovery/registry artifacts for the Entalpa MCP server.

## Plugin Bundle

The plugin bundle lives at `plugins/entalpa` and includes:

- Codex manifest: `plugins/entalpa/.codex-plugin/plugin.json`
- Claude Code manifest: `plugins/entalpa/.claude-plugin/plugin.json`
- Codex MCP config: `plugins/entalpa/.codex-mcp.json`
- Claude Code MCP config: `plugins/entalpa/.mcp.json`
- Skill: `plugins/entalpa/skills/entalpa-implement/SKILL.md`
- Skill: `plugins/entalpa/skills/entalpa-prd/SKILL.md`

The plugin installs the Entalpa MCP server and all configured skills together: `entalpa-implement`, `entalpa-prd`.

The unpinned marketplace commands below read `entalpa/entalpa-mcp`'s default branch. Use the pinned release commands in [release-and-versioning.md](release-and-versioning.md) when you need a reproducible version.

## Codex

Add the repository marketplace:

```bash
codex plugin marketplace add entalpa/entalpa-mcp --sparse .agents/plugins --sparse plugins
```

Then open `/plugins` in Codex, choose the Entalpa Plugins marketplace, and install/enable `entalpa`.

## Claude Code

Add the repository marketplace:

```bash
claude plugin marketplace add entalpa/entalpa-mcp --sparse .claude-plugin plugins
```

Install the plugin:

```bash
claude plugin install entalpa@entalpa-plugins
```

After installing or enabling a plugin in an active Claude Code session, restart Claude Code or run `/reload-plugins` before verifying MCP tools.

## Discovery

Use native installers and the plugin marketplaces above. Registry and directory listings are documented here only after publication and verification.

## Sources

- [Codex Plugins](https://learn.chatgpt.com/docs/plugins)
- [Build Codex plugins](https://developers.openai.com/plugins/build/plugins)
- [Claude Code plugin marketplaces](https://code.claude.com/docs/en/plugin-marketplaces)
- [Claude Code plugins reference](https://code.claude.com/docs/en/plugins-reference)
- [MCP Registry](https://modelcontextprotocol.io/registry/about)
- [Configure MCP servers for GitHub Copilot coding agent](https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/configure-mcp-servers)
- [Smithery publish MCP servers](https://smithery.ai/docs/build/publish)
- [Glama MCP directory](https://glama.ai/)
- [mcp.so MCP directory](https://mcp.so/)
