# Gemini CLI

<!-- Generated from Entalpa's canonical integration source. -->

Use this legacy path only where Gemini CLI still serves the account's authentication tier; affected individual users should migrate the same MCP and skills workflow to Antigravity CLI.

## Requirements

- Gemini CLI installed.
- Browser access for OAuth if prompted by the MCP client.
- An authentication route that still serves Gemini CLI, such as an eligible organization license, Gemini API key, or Vertex AI configuration.

## Install MCP Server

### Add the MCP server

```bash
gemini mcp add --transport http entalpa https://api.entalpa.com/mcp
```

### Manual settings fallback

```json
{
  "mcpServers": {
    "entalpa": {
      "httpUrl": "https://api.entalpa.com/mcp",
      "timeout": 30000
    }
  }
}
```

## Install Entalpa Skill

Install from `entalpa/entalpa-mcp`'s default branch for the latest skill, or use a release tag for a reproducible install.

### Install the Entalpa skills natively

```bash
gemini skills install https://github.com/entalpa/entalpa-mcp.git --path skills/entalpa-implement --consent
gemini skills install https://github.com/entalpa/entalpa-mcp.git --path skills/entalpa-prd --consent
```

### Skills CLI alternative

```bash
npx skills add entalpa/entalpa-mcp --skill "*" --agent gemini-cli -g -y
```

### GitHub CLI alternative

```bash
gh skill install entalpa/entalpa-mcp entalpa-implement --agent gemini-cli --scope user
gh skill install entalpa/entalpa-mcp entalpa-prd --agent gemini-cli --scope user
```

## Verify

- Run `gemini mcp list` or use `/mcp` in Gemini CLI to confirm Entalpa is connected.
- Use `/mcp auth entalpa` if authentication is pending.

## Known Limitations

- Gemini CLI uses `httpUrl` for Streamable HTTP and `url` for SSE; do not swap these fields.
- Gemini CLI stopped serving requests for Gemini Code Assist for individuals, Google AI Pro, and Google AI Ultra on June 18, 2026. Those users should use the Antigravity guide; do not present Gemini CLI as a new-install path for those plans.

## Sources

- [Gemini CLI MCP servers](https://geminicli.com/docs/tools/mcp-server/)
- [Gemini CLI settings](https://geminicli.com/docs/reference/configuration/)
- [Gemini CLI Agent Skills](https://geminicli.com/docs/cli/skills/)
- [npx skills](https://github.com/vercel-labs/skills)
- [GitHub CLI skills](https://cli.github.com/manual/gh_skill)
