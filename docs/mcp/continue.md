# Continue

<!-- Generated from Entalpa's canonical integration source. -->

Continue supports MCP blocks and remote HTTP-based transports. Add Entalpa through Continue MCP configuration, then use Entalpa server instructions for workflow guidance.

## Requirements

- Continue installed with Agent Mode enabled.
- Browser access for OAuth if the current Continue build supports OAuth for remote MCP.

## Install MCP Server

### Add remote MCP config

```yaml
mcpServers:
  - name: entalpa
    type: streamable-http
    url: https://api.entalpa.com/mcp
```

### Standalone MCP server block

If you use a `.continue/mcpServers/entalpa.yaml` block instead of inline config, include Continue's required block metadata such as `name`, `version`, and `schema` alongside the server definition.

### SSE compatibility fallback

If the installed Continue version only exposes SSE examples, do not force Entalpa through SSE unless Entalpa publishes a compatible SSE endpoint.

## Install Entalpa Skill

Install from `entalpa/entalpa-mcp`'s default branch for the latest skill, or use a release tag for a reproducible install.

### Use server instructions

Continue's official MCP docs do not document local Agent Skills installation. Use the Entalpa MCP server instructions and these docs as the workflow guide until runtime skill loading is validated.

## Verify

- Switch Continue to Agent Mode and confirm Entalpa tools appear.

## Known Limitations

- Continue's MCP configuration format has changed over time. Treat exact YAML keys as version-specific and validate before sharing a team config.

## Sources

- [Continue MCP deep dive](https://docs.continue.dev/customize/deep-dives/mcp)
- [Continue MCP servers](https://docs.continue.dev/customize/mcp-tools)
