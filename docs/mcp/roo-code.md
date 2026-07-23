# Roo Code

<!-- Generated from Entalpa's canonical integration source. -->

Roo Code supports Streamable HTTP MCP configuration through global or project MCP settings. Use Entalpa's remote URL and server instructions.

## Requirements

- Roo Code VS Code extension installed.
- Browser access for OAuth.

## Install MCP Server

### Add through Roo MCP settings

Open Roo Code MCP settings, choose Edit Global MCP or Edit Project MCP, and add the Entalpa server.

### Project config

```json
{
  "mcpServers": {
    "entalpa": {
      "type": "streamable-http",
      "url": "https://api.entalpa.com/mcp"
    }
  }
}
```

## Install Entalpa Skill

Install from `entalpa/entalpa-mcp`'s default branch for the latest skill, or use a release tag for a reproducible install.

### Install the Entalpa skills

```bash
npx skills add entalpa/entalpa-mcp --skill "*" --agent roo -g -y
```

## Verify

- Confirm Entalpa appears in the Roo Code MCP server list.
- Ask Roo to list Entalpa projects and approve the tool call.

## Known Limitations

- Roo Code documentation has moved to a legacy/static site and the project status should be reviewed before treating Roo as an active first-class path.
- OAuth behavior for remote Streamable HTTP should be validated in the installed Roo Code version before moving this to Tier 1.

## Sources

- [Roo Code MCP](https://roocodeinc.github.io/Roo-Code/features/mcp/overview/)
- [Roo Code MCP transports](https://roocodeinc.github.io/Roo-Code/features/mcp/server-transports/)
- [npx skills](https://github.com/vercel-labs/skills)
