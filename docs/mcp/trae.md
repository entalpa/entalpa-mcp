# Trae

<!-- Generated from Entalpa's canonical integration source. -->

Use Trae's native MCP settings or install-link flow for the Entalpa remote server, then install the Entalpa skills through Trae's SKILL.md paths.

## Requirements

- Trae IDE version with MCP and Skills support.
- Browser access for OAuth if Trae prompts for Entalpa authorization.

## Install MCP Server

### Add through Trae MCP settings

Open Trae settings, select MCP, add a custom server named `entalpa`, and use URL `https://api.entalpa.com/mcp` with the remote HTTP transport option available in your Trae build.

### Install-link candidate

Trae supports MCP server install links generated from JSON configuration. Generate and publish an Entalpa install link only after validating Trae's current remote Streamable HTTP and OAuth behavior.

### Manual config fallback

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

### Install the Entalpa skills with Skills CLI

```bash
npx skills add entalpa/entalpa-mcp --skill "*" --agent trae -g -y
```

### Trae CN Skills CLI alternative

```bash
npx skills add entalpa/entalpa-mcp --skill "*" --agent trae-cn -g -y
```

### Manual project skills fallback

```bash
tmpdir="$(mktemp -d)"
git clone --depth 1 https://github.com/entalpa/entalpa-mcp.git "$tmpdir"
mkdir -p .trae/skills
cp -R "$tmpdir/skills/." .trae/skills/
```

### Trae UI alternative

Trae can import a `SKILL.md` file or a ZIP containing `SKILL.md`. Import `skills/entalpa-implement` and `skills/entalpa-prd` separately when you want a UI-based install.

## Verify

- Restart Trae or reload MCP servers and confirm Entalpa tools are available in Agent mode.
- Ask Trae to call `users_get_me` or list Entalpa projects.
- Confirm both Entalpa skills appear in Trae's Skills list or are available from `.trae/skills`.

## Known Limitations

- Trae UI labels and install-link behavior are version-sensitive; validate before sharing an install link.
- Trae's official setup docs establish remote MCP configuration but do not verify Entalpa's OAuth flow. Keep direct and install-link OAuth marked untested until runtime validation succeeds.

## Sources

- [Trae MCP overview](https://docs.trae.ai/ide/model-context-protocol)
- [Trae add MCP servers](https://docs.trae.ai/ide/add-mcp-servers)
- [Trae MCP server install links](https://docs.trae.ai/ide/mcp-server-install-links)
- [Trae skills](https://docs.trae.ai/ide/skills)
- [npx skills](https://github.com/vercel-labs/skills)
