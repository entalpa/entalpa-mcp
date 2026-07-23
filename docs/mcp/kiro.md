# Kiro

<!-- Generated from Entalpa's canonical integration source. -->

Use Kiro's official one-click MCP link or add Entalpa through workspace or user MCP configuration, then install the skills in Kiro's native skills path.

## Requirements

- Kiro with MCP support.
- Browser access for OAuth.

## Install MCP Server

### One-click Add to Kiro path

Open `https://kiro.dev/launch/mcp/add?name=entalpa&config=%7B%22url%22%3A%22https%3A%2F%2Fapi.entalpa.com%2Fmcp%22%2C%22disabled%22%3Afalse%7D`, review the remote-server configuration, and approve the browser OAuth flow.

### Add through Kiro MCP settings

Use Command Palette `Kiro: Open workspace MCP config (JSON)`, `Kiro: Open user MCP config (JSON)`, or the Kiro panel Open MCP Config icon, then add a remote MCP server named `entalpa`.

### Manual workspace config

```json
{
  "mcpServers": {
    "entalpa": {
      "url": "https://api.entalpa.com/mcp",
      "disabled": false
    }
  }
}
```

## Install Entalpa Skill

Install from `entalpa/entalpa-mcp`'s default branch for the latest skill, or use a release tag for a reproducible install.

### Native Kiro skill path

Import each canonical folder URL under `skills/` through Kiro's Skills UI, or place both skill folders under `.kiro/skills` for the workspace or `~/.kiro/skills` for the user. Use the published repository folder URL for UI-based installation.

### Portable Skills CLI fallback

```bash
npx skills add entalpa/entalpa-mcp --skill "*" --agent kiro-cli -g -y
```

## Verify

- Confirm Kiro shows the Entalpa MCP server as connected and can list projects.

## Known Limitations

- The one-click link installs the MCP configuration, not the Entalpa skills; install and verify the skills separately.

## Sources

- [Kiro MCP server directory](https://kiro.dev/docs/mcp/servers/)
- [Kiro MCP configuration](https://kiro.dev/docs/mcp/configuration/)
- [Kiro Skills](https://kiro.dev/docs/skills/)
- [npx skills](https://github.com/vercel-labs/skills)
