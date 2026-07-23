# Devin

<!-- Generated from Entalpa's canonical integration source. -->

Add Entalpa to hosted Devin through its MCP Marketplace, or use Devin CLI for local sessions, and commit the Entalpa skills under Devin's recommended `.agents/skills` path.

## Requirements

- Devin account with permission to add organization or personal MCP servers, or Devin CLI installed and signed in.
- Browser access for OAuth.

## Install MCP Server

### Hosted Devin MCP path

Open Settings, MCP Marketplace, select Add Your Own, choose HTTP, set server name `entalpa` and Server URL `https://api.entalpa.com/mcp`, then choose OAuth as the authentication method.

### Complete hosted OAuth

An organization admin completes the browser authorization flow when Devin prompts during installation or first use. Use a personal MCP server only when authorization must remain user-specific.

### Add the MCP server

```bash
devin mcp add entalpa https://api.entalpa.com/mcp
```

### Authenticate

```bash
devin mcp login entalpa
```

### Shared project config

```json
{
  "mcpServers": {
    "entalpa": {
      "url": "https://api.entalpa.com/mcp",
      "transport": "http"
    }
  }
}
```

## Install Entalpa Skill

Install from `entalpa/entalpa-mcp`'s default branch for the latest skill, or use a release tag for a reproducible install.

### Install the repository skills for hosted and local Devin

```bash
tmpdir="$(mktemp -d)"
git clone --depth 1 https://github.com/entalpa/entalpa-mcp.git "$tmpdir"
mkdir -p .agents/skills
cp -R "$tmpdir/skills/." .agents/skills/
```

## Verify

- Run `devin mcp list` and confirm `entalpa` is configured.
- Ask Devin to list Entalpa projects.

## Known Limitations

- Hosted Devin organization OAuth is shared and admin-controlled, while personal MCP authorization is user-specific. Validate Entalpa's selected scope before rollout.
- Entalpa OAuth remains runtime-unverified in hosted Devin; keep the CLI path available during validation.

## Sources

- [Devin hosted MCP servers](https://docs.devin.ai/work-with-devin/mcp)
- [Devin CLI MCP configuration](https://docs.devin.ai/cli/extensibility/mcp/configuration)
- [Devin product skills](https://docs.devin.ai/product-guides/skills)
- [Devin skills](https://docs.devin.ai/cli/extensibility/skills/overview)
