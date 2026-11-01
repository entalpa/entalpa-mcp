# Claude Code

<!-- Generated from Entalpa's canonical integration source. -->

Install the Entalpa plugin from Claude's plugin directory to get MCP plus all skills together, or use Claude Code's native MCP command when you only want the remote server.

## Requirements

- Claude Code installed and signed in.
- Browser access for the OAuth authorization flow.
- For the directory install, Claude Code 2.1.287 or later.

## Install MCP Server

### Add the MCP server

```bash
claude mcp add --transport http entalpa https://api.entalpa.com/mcp
```

### Start Claude Code and approve OAuth

Start Claude Code, run `/mcp`, select `entalpa`, and follow the browser authorization flow.

## Install Entalpa Skill

Install from `entalpa/entalpa-mcp`'s default branch for the latest skill, or use a release tag for a reproducible install.

### Preferred plugin path

Entalpa is listed in Claude's plugin directory, which Claude Code knows as the built-in `anthropic-plugin-directory` marketplace. Install it from your shell, or run `/plugin directory entalpa` in a session.

```bash
claude plugin install entalpa@anthropic-plugin-directory
```

### Added on claude.ai

If you added Entalpa in claude.ai or the Claude desktop app, there is nothing to install. Claude Code 2.1.273 or later loads it from your account as `entalpa@synced` in sessions signed in with that Claude account.

### Plugin marketplace alternative

On Claude Code older than 2.1.287, or where your organization blocks the directory, use the Entalpa marketplace.

```bash
claude plugin marketplace add entalpa/entalpa-mcp --sparse .claude-plugin plugins
claude plugin install entalpa@entalpa-plugins
```

### Install the Entalpa skills

```bash
npx skills add entalpa/entalpa-mcp --skill "*" --agent claude-code -g -y
```

### GitHub CLI alternative

```bash
gh skill install entalpa/entalpa-mcp entalpa-implement --agent claude-code --scope user
gh skill install entalpa/entalpa-mcp entalpa-prd --agent claude-code --scope user
gh skill install entalpa/entalpa-mcp entalpa-openspec --agent claude-code --scope user
gh skill install entalpa/entalpa-mcp entalpa-speckit --agent claude-code --scope user
```

## Verify

- After installing or enabling the plugin, restart Claude Code or run `/reload-plugins`.
- The Installed tab of `/plugin` lists the plugin as `entalpa@anthropic-plugin-directory` (directory install), `entalpa@synced` (added on claude.ai) or `entalpa@entalpa-plugins` (Entalpa marketplace).
- The plugin's server appears in `/mcp` as `plugin:entalpa:entalpa`. Select it and follow the browser authorization flow.
- Ask Claude Code to list Entalpa projects.
- If the browser does not open, copy the URL from `/mcp` and open it manually. Use `--callback-port` only for fixed pre-registered redirect URIs.

## Known Limitations

- The plugin path bundles the MCP server and all skills. The native `claude mcp add` command remains useful when users only want MCP without plugin packaging.
- Install the plugin one way only. An installed copy takes precedence over the one synced from claude.ai, which Claude Code then reports as not loaded.

## Sources

- [Claude Code MCP](https://code.claude.com/docs/en/mcp)
- [Plugin feature support across platforms](https://claude.com/docs/plugins/platform-support)
- [Plugins in Claude](https://claude.com/docs/plugins/overview)
- [Claude Code plugins synced from claude.ai](https://code.claude.com/docs/en/plugins/loading#synced-plugins)
- [Claude Code plugin marketplaces](https://code.claude.com/docs/en/plugin-marketplaces)
- [Claude Code plugins reference](https://code.claude.com/docs/en/plugins-reference)
- [Use plugins in Claude](https://support.claude.com/en/articles/13837440-use-plugins-in-claude)
- [npx skills](https://github.com/vercel-labs/skills)
- [GitHub CLI skills](https://cli.github.com/manual/gh_skill)
