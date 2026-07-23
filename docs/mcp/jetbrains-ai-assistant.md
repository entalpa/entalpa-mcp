# JetBrains AI Assistant

<!-- Generated from Entalpa's canonical integration source. -->

JetBrains AI Assistant can configure HTTP MCP servers, but its current direct client does not complete Entalpa's OAuth flow; use only a separately validated stdio bridge candidate.

## Requirements

- JetBrains IDE with AI Assistant MCP support.
- Node.js and `npx` for the `mcp-remote` bridge candidate.
- Browser access for OAuth through the bridge.

## Install MCP Server

### Open JetBrains MCP settings

Open Settings, Tools, AI Assistant, Model Context Protocol, then add a server configuration.

### Stdio bridge candidate

```json
{
  "mcpServers": {
    "entalpa": {
      "command": "npx",
      "args": [
        "-y",
        "mcp-remote",
        "https://api.entalpa.com/mcp"
      ]
    }
  }
}
```

## Install Entalpa Skill

Install from `entalpa/entalpa-mcp`'s default branch for the latest skill, or use a release tag for a reproducible install.

### Native skill settings

JetBrains AI Assistant documents native skill sources and settings for supported JetBrains agent surfaces, but `npx skills` does not currently list a JetBrains target. Use the native JetBrains Skills settings after validating the target IDE and agent surface.

## Verify

- Apply the MCP settings and confirm JetBrains shows the server as connected.
- Ask AI Assistant to list Entalpa projects.

## Known Limitations

- Direct JetBrains AI Assistant HTTP MCP authentication is unsupported for Entalpa while the upstream OAuth issue remains open.
- The `mcp-remote` workaround is documented by JetBrains for authenticated HTTP servers but has not been runtime-tested with Entalpa; do not present this as direct native OAuth.

## Sources

- [JetBrains AI Assistant MCP](https://www.jetbrains.com/help/ai-assistant/mcp.html)
- [JetBrains MCP OAuth support issue](https://youtrack.jetbrains.com/issue/LLM-25012/OAuth2-Authentication-for-MCP-Server-Connections)
- [JetBrains AI Assistant skills](https://www.jetbrains.com/help/ai-assistant/agent-skills.html)
- [JetBrains AI Assistant skills settings](https://www.jetbrains.com/help/ai-assistant/settings-reference-skills.html)
- [npx skills](https://github.com/vercel-labs/skills)
