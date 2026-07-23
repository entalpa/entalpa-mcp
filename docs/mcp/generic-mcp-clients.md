# Generic MCP Clients

<!-- Generated from Entalpa's canonical integration source. -->

Use this page only when your client is not covered by a dedicated Entalpa guide and does not provide a native installer for remote MCP servers.

## Server Details

- Name: `entalpa`
- URL: `https://api.entalpa.com/mcp`
- Transport: Streamable HTTP
- Authentication: OAuth through Entalpa/Keycloak

## Common Config Shapes

Some clients use this remote HTTP shape:

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

Other clients require `httpUrl` for Streamable HTTP:

```json
{
  "mcpServers": {
    "entalpa": {
      "httpUrl": "https://api.entalpa.com/mcp"
    }
  }
}
```

Cline-style clients can require an explicit Streamable HTTP transport key:

```json
{
  "mcpServers": {
    "entalpa": {
      "type": "streamableHttp",
      "url": "https://api.entalpa.com/mcp"
    }
  }
}
```

VS Code workspace MCP config uses a top-level `servers` object:

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

## Generic Installer

When the target agent is supported by `add-mcp`, this command can write the correct config shape:

```bash
npx add-mcp https://api.entalpa.com/mcp --name entalpa --transport http
```

## Skills

If the target agent is supported by `npx skills`, install all Entalpa skills:

This installs from `entalpa/entalpa-mcp`'s default branch. Use a release tag when you need a reproducible version.

```bash
npx skills add entalpa/entalpa-mcp --skill "*" --agent <agent> -g -y
```

Check the [supported-agent table in the Skills CLI repository](https://github.com/vercel-labs/skills#supported-agents) before changing `<agent>`. The command's `--help` output lists flags, not the complete agent table.

## Sources

- [add-mcp](https://github.com/neon-solutions/add-mcp)
- [npx skills](https://github.com/vercel-labs/skills)
- [VS Code MCP configuration reference](https://code.visualstudio.com/docs/agents/reference/mcp-configuration)
- [Gemini CLI MCP servers](https://geminicli.com/docs/tools/mcp-server/)
- [Cline MCP](https://docs.cline.bot/mcp/mcp-overview)
