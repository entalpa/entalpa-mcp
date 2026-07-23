# Cline

<!-- Generated from Entalpa's canonical integration source. -->

Use Cline's Remote Servers tab or MCP settings JSON, then install the Entalpa skills in Cline's documented skills paths.

## Requirements

- Cline extension or Cline CLI installed.
- Browser access for OAuth.

## Install MCP Server

### Add through Cline Remote Servers

Open the Cline MCP Servers panel, choose the Remote Servers tab, enter server name `entalpa`, choose Streamable HTTP, and use URL `https://api.entalpa.com/mcp`.

### Manual config

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

### Community installer fallback for Cline extension

```bash
npx add-mcp https://api.entalpa.com/mcp --name entalpa --transport http --agent cline --global -y
```

### Community installer fallback for Cline CLI

```bash
npx add-mcp https://api.entalpa.com/mcp --name entalpa --transport http --agent cline-cli --global -y
```

## Install Entalpa Skill

Install from `entalpa/entalpa-mcp`'s default branch for the latest skill, or use a release tag for a reproducible install.

### Install as Cline project skills

```bash
tmpdir="$(mktemp -d)"
git clone --depth 1 https://github.com/entalpa/entalpa-mcp.git "$tmpdir"
mkdir -p .cline/skills
cp -R "$tmpdir/skills/." .cline/skills/
```

### Install as Cline user skills

```bash
tmpdir="$(mktemp -d)"
git clone --depth 1 https://github.com/entalpa/entalpa-mcp.git "$tmpdir"
mkdir -p ~/.cline/skills
cp -R "$tmpdir/skills/." ~/.cline/skills/
```

### Skills CLI compatibility target

The current Skills CLI `cline` target writes `.agents/skills`, which is not listed in Cline's official skill paths. Use it only after validating the installed Cline version loads that compatibility path.

## Verify

- Confirm Entalpa appears in Cline's MCP server list.
- Ask Cline to call `users_get_me` or list projects.

## Known Limitations

- Use the marketplace only after Entalpa is accepted there. Treat `add-mcp` as a community fallback and validate generated config before sharing it with a team.

## Sources

- [Cline MCP](https://docs.cline.bot/mcp/mcp-overview)
- [add-mcp](https://github.com/neon-solutions/add-mcp)
- [Cline Skills](https://docs.cline.bot/customization/skills)
- [npx skills](https://github.com/vercel-labs/skills)
