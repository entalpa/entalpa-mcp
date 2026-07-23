# Google Antigravity

<!-- Generated from Entalpa's canonical integration source. -->

Configure Entalpa in Antigravity's dedicated MCP profile with the current `serverUrl` key, then install the skills in the matching user or workspace scope.

## Requirements

- Google Antigravity IDE or CLI installed.
- Browser access for OAuth if the client prompts for Entalpa authorization.

## Install MCP Server

### Open the dedicated MCP profile

In Antigravity IDE, open the agent panel menu, choose MCP Servers, Manage MCP Servers, then View raw config. Use global `~/.gemini/config/mcp_config.json` or workspace `.agents/mcp_config.json`; Antigravity CLI uses the same paths.

### Configure the remote server

```json
{
  "mcpServers": {
    "entalpa": {
      "serverUrl": "https://api.entalpa.com/mcp"
    }
  }
}
```

### Authenticate

Open Agent Settings, Customizations, select Authenticate for `entalpa`, complete the browser flow, and paste the returned authorization code when prompted.

## Install Entalpa Skill

Install from `entalpa/entalpa-mcp`'s default branch for the latest skill, or use a release tag for a reproducible install.

### Install the Entalpa skills

```bash
npx skills add entalpa/entalpa-mcp --skill "*" --agent antigravity -g -y
```

## Verify

- Ask Antigravity to list available Entalpa tools or projects.
- Confirm the server remains enabled after restarting the IDE or CLI.

## Known Limitations

- Remote Antigravity MCP entries require `serverUrl`; legacy `url` and `httpUrl` keys are not supported.
- Entalpa OAuth should remain marked runtime-unverified until the authorization-code handoff has been tested in the target Antigravity build.

## Sources

- [Google Antigravity MCP](https://antigravity.google/docs/mcp)
- [Google Antigravity Agent Skills](https://antigravity.google/docs/skills?app=antigravity-ide)
- [npx skills](https://github.com/vercel-labs/skills)
