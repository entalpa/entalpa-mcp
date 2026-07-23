# Claude Code

<!-- Generated from Entalpa's canonical integration source. -->

Use the Entalpa Claude Code plugin to install MCP plus all skills together, or use Claude Code's native MCP command when you only want the remote server.

## Requirements

- Claude Code installed and signed in.
- Browser access for the OAuth authorization flow.

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
```

## Verify

- After installing or enabling the plugin, restart Claude Code or run `/reload-plugins`.
- Ask Claude Code to list Entalpa projects.
- If the browser does not open, copy the URL from `/mcp` and open it manually. Use `--callback-port` only for fixed pre-registered redirect URIs.

## Known Limitations

- The plugin path bundles the MCP server and all skills. The native `claude mcp add` command remains useful when users only want MCP without plugin packaging.

## Sources

- [Claude Code MCP](https://code.claude.com/docs/en/mcp)
- [Claude Code plugin marketplaces](https://code.claude.com/docs/en/plugin-marketplaces)
- [Claude Code plugins reference](https://code.claude.com/docs/en/plugins-reference)
- [Use plugins in Claude](https://support.claude.com/en/articles/13837440-use-plugins-in-claude)
- [npx skills](https://github.com/vercel-labs/skills)
- [GitHub CLI skills](https://cli.github.com/manual/gh_skill)
