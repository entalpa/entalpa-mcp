# Tencent CodeBuddy

<!-- Generated from Entalpa's canonical integration source. -->

Use CodeBuddy's native MCP CLI or JSON config for the Entalpa HTTP server, then install the Entalpa skills through CodeBuddy's skill directories.

## Requirements

- CodeBuddy Code CLI installed and authenticated.
- Browser access for OAuth if prompted by the remote MCP server.

## Install MCP Server

### Add the MCP server

```bash
codebuddy mcp add --scope user --transport http entalpa https://api.entalpa.com/mcp
```

### JSON config alternative

```bash
codebuddy mcp add-json --scope user entalpa '{"type":"http","url":"https://api.entalpa.com/mcp"}'
```

### Manual config fallback

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

## Install Entalpa Skill

Install from `entalpa/entalpa-mcp`'s default branch for the latest skill, or use a release tag for a reproducible install.

### Install the Entalpa skills with Skills CLI

```bash
npx skills add entalpa/entalpa-mcp --skill "*" --agent codebuddy -g -y
```

### Manual user skills fallback

```bash
tmpdir="$(mktemp -d)"
git clone --depth 1 https://github.com/entalpa/entalpa-mcp.git "$tmpdir"
mkdir -p ~/.codebuddy/skills
cp -R "$tmpdir/skills/." ~/.codebuddy/skills/
```

### Project skills alternative

```bash
tmpdir="$(mktemp -d)"
git clone --depth 1 https://github.com/entalpa/entalpa-mcp.git "$tmpdir"
mkdir -p .codebuddy/skills
cp -R "$tmpdir/skills/." .codebuddy/skills/
```

### Plugin package candidate

Adapt the Entalpa bundle to CodeBuddy's plugin manifest and validate that the plugin loads both the Skill and MCP definition. A plugin is the installable package; it is not itself a marketplace.

### Marketplace publication candidate

After the plugin package and OAuth behavior pass validation, publish or register a CodeBuddy marketplace that lists the plugin. The marketplace is only the discovery catalog for the packaged plugin.

## Verify

- Run `codebuddy mcp list` or `codebuddy mcp get entalpa` to confirm Entalpa is connected.
- Ask CodeBuddy to call `users_get_me` or list Entalpa projects.
- Confirm both Entalpa skills appear after starting a new CodeBuddy session.

## Known Limitations

- CodeBuddy documents remote HTTP configuration but does not clearly establish automatic OAuth discovery. Do not mark Entalpa connected until the browser authorization and token refresh flow pass runtime testing.
- CodeBuddy plugin packaging and marketplace publication are separate validation and distribution steps; neither replaces direct MCP and skill setup until accepted and tested.

## Sources

- [CodeBuddy MCP](https://www.codebuddy.ai/docs/cli/mcp)
- [CodeBuddy skills](https://www.codebuddy.ai/docs/cli/skills)
- [npx skills](https://github.com/vercel-labs/skills)
- [CodeBuddy plugins](https://www.codebuddy.ai/docs/cli/plugins)
- [CodeBuddy plugin marketplaces](https://www.codebuddy.ai/docs/cli/plugin-marketplaces)
