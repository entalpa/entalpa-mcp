# Cursor

<!-- Generated from Entalpa's canonical integration source. -->

Use Cursor's self-service Add to Cursor link for one-click MCP setup, with MCP settings or `.cursor/mcp.json` as fallbacks, then install the skills separately.

## Requirements

- Cursor version with remote MCP and OAuth support.
- Browser access for OAuth.

## Install MCP Server

### One-click Add to Cursor path

Open `cursor://anysphere.cursor-deeplink/mcp/install?name=entalpa&config=eyJ1cmwiOiJodHRwczovL2FwaS5lbnRhbHBhLmNvbS9tY3AifQ`, review the remote-server configuration, and complete OAuth when Cursor prompts.

### Add through Cursor settings

Open Cursor Customize, then MCP, add a new remote server named `entalpa`, and use URL `https://api.entalpa.com/mcp`. You can also edit project `.cursor/mcp.json` or global `~/.cursor/mcp.json`.

### Manual project config

```json
{
  "mcpServers": {
    "entalpa": {
      "url": "https://api.entalpa.com/mcp"
    }
  }
}
```

## Install Entalpa Skill

Install from `entalpa/entalpa-mcp`'s default branch for the latest skill, or use a release tag for a reproducible install.

### Install the Entalpa skills

```bash
npx skills add entalpa/entalpa-mcp --skill "*" --agent cursor -g -y
```

### GitHub CLI alternative

```bash
gh skill install entalpa/entalpa-mcp entalpa-implement --agent cursor --scope user
gh skill install entalpa/entalpa-mcp entalpa-prd --agent cursor --scope user
```

## Verify

- Reload Cursor and confirm Entalpa appears in MCP tools.
- Ask Cursor to call `users_get_me` or list projects.

## Known Limitations

- Keep manual settings available when workspace policy blocks deep links, and retain OAuth runtime validation before treating the published one-click link as the only path.

## Sources

- [Cursor MCP one-click install and OAuth](https://cursor.com/changelog/1-0)
- [Cursor MCP](https://cursor.com/docs/mcp)
- [npx skills](https://github.com/vercel-labs/skills)
- [GitHub CLI skills](https://cli.github.com/manual/gh_skill)
