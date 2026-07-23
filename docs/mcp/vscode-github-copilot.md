# VS Code and GitHub Copilot

<!-- Generated from Entalpa's canonical integration source. -->

Prefer the Entalpa agent plugin shared with Copilot CLI, or use the VS Code MCP server gallery or `.vscode/mcp.json` for direct setup.

## Requirements

- VS Code with Copilot Chat agent mode and MCP support enabled.
- Browser access for OAuth.

## Install MCP Server

### Add through VS Code

Use Command Palette `MCP: Add Server`, select HTTP, and enter `https://api.entalpa.com/mcp` with server name `entalpa`.

### Manual workspace config

```json
{
  "servers": {
    "entalpa": {
      "type": "http",
      "url": "https://api.entalpa.com/mcp"
    }
  }
}
```

## Install Entalpa Skill

Install from `entalpa/entalpa-mcp`'s default branch for the latest skill, or use a release tag for a reproducible install.

### Preferred Copilot plugin path

```bash
copilot plugin marketplace add entalpa/entalpa-mcp
copilot plugin install entalpa@entalpa-plugins
```

### Enable the plugin in VS Code

VS Code discovers plugins installed under `~/.copilot/installed-plugins`. Open the Agent Plugins installed view, review the Entalpa plugin, and enable it for the desired profile or workspace.

### GitHub CLI skill alternative

```bash
gh skill install entalpa/entalpa-mcp entalpa-implement --agent github-copilot --scope user
gh skill install entalpa/entalpa-mcp entalpa-prd --agent github-copilot --scope user
```

### npx skills alternative

```bash
npx skills add entalpa/entalpa-mcp --skill "*" --agent github-copilot -g -y
```

## Verify

- Restart MCP servers from the VS Code MCP view and confirm Entalpa tools appear.
- Ask Copilot Chat to list Entalpa projects.

## Known Limitations

- GitHub Copilot coding agent and code review repository MCP config is not documented here for Entalpa because GitHub currently documents OAuth limitations for remote MCP on that surface.

## Sources

- [VS Code MCP servers](https://code.visualstudio.com/docs/agent-customization/mcp-servers)
- [Extend Copilot Chat with MCP](https://docs.github.com/en/copilot/how-tos/provide-context/use-mcp-in-your-ide/extend-copilot-chat-with-mcp)
- [Configure MCP servers for GitHub Copilot coding agent](https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/configure-mcp-servers)
- [VS Code MCP configuration reference](https://code.visualstudio.com/docs/agents/reference/mcp-configuration)
- [GitHub Copilot CLI plugin reference](https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-plugin-reference)
- [Agent plugins in VS Code](https://code.visualstudio.com/docs/agent-customization/agent-plugins)
- [GitHub CLI skills](https://cli.github.com/manual/gh_skill)
- [npx skills](https://github.com/vercel-labs/skills)
