# Amazon Q Developer for Existing IDE Customers

<!-- Generated from Entalpa's canonical integration source. -->

Use this transitional path only for existing Amazon Q Developer IDE customers. The Q CLI is now Kiro CLI, so command-line users should follow the Kiro guide.

## Requirements

- Existing Amazon Q Developer IDE extension access established before new sign-ups closed on May 15, 2026.
- Browser access for OAuth.

## Install MCP Server

### Add through Amazon Q IDE MCP UI

Open the Amazon Q MCP configuration UI, add an HTTP MCP server named `entalpa`, and set the URL to `https://api.entalpa.com/mcp`.

### Remote HTTP config

```json
{
  "mcpServers": {
    "entalpa": {
      "type": "http",
      "url": "https://api.entalpa.com/mcp"
    }
  }
}
```

### Amazon Q IDE config locations

For Q in the IDE, use global `~/.aws/amazonq/default.json` or project `.amazonq/default.json` depending on the desired scope.

## Install Entalpa Skill

Install from `entalpa/entalpa-mcp`'s default branch for the latest skill, or use a release tag for a reproducible install.

### Route new CLI and skill setup to Kiro

The Amazon Q Developer CLI was rebranded as Kiro CLI. Use the Kiro guide for current CLI MCP and skill installation instead of creating a new Q CLI configuration.

## Verify

- Use `/mcp` to authenticate if prompted, then use `/tools` in Amazon Q to confirm Entalpa tools are loaded.
- Ask Q to call `users_get_me` or list projects.

## Known Limitations

- Keep credentials out of project config. Use Q's supported secret handling for any future static credentials.
- Amazon Q Developer IDE plugins and paid subscriptions reach end of support on April 30, 2027. Existing customers retain IDE access during the transition; new users should start with Kiro.

## Sources

- [Amazon Q Developer MCP](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/qdev-mcp.html)
- [Amazon Q Developer IDE MCP configuration](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/mcp-ide.html)
- [Amazon Q Developer CLI MCP configuration](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/command-line-mcp-config-CLI.html)
- [Amazon Q Developer end-of-support announcement](https://aws.amazon.com/blogs/devops/amazon-q-developer-end-of-support-announcement/)
- [Upgrade from Amazon Q Developer CLI to Kiro](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/upgrade-to-kiro.html)
- [Kiro Skills](https://kiro.dev/docs/skills/)
