# Augment Code

<!-- Generated from Entalpa's canonical integration source. -->

Use Auggie's native MCP command or Augment's remote MCP UI, then place the Entalpa skills in Augment's native Agent Skills path.

## Requirements

- Augment Code installed.
- Browser access if the installed Augment surface can complete Entalpa OAuth.

## Install MCP Server

### Add with Auggie CLI

```bash
auggie mcp add entalpa --transport http --url https://api.entalpa.com/mcp
```

### Add a remote MCP server

In Augment settings, choose Add remote MCP, select HTTP, name the server `entalpa`, and enter `https://api.entalpa.com/mcp`.

### Import JSON alternative

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

### Install in Augment's native user skills path

```bash
tmpdir="$(mktemp -d)"
git clone --depth 1 https://github.com/entalpa/entalpa-mcp.git "$tmpdir"
mkdir -p ~/.augment/skills
cp -R "$tmpdir/skills/." ~/.augment/skills/
```

### Skills CLI alternative

```bash
npx skills add entalpa/entalpa-mcp --skill "*" --agent augment -g -y
```

## Verify

- Confirm Augment shows Entalpa as connected and can list projects.

## Known Limitations

- Augment's review-agent MCP setup is distinct from local IDE setup; validate the target surface before publishing team instructions.
- Augment documents remote HTTP servers and static headers, but its current docs do not establish automatic MCP OAuth discovery. Keep Entalpa authentication runtime-unverified until tested in the target build.

## Sources

- [Auggie integrations and MCP](https://docs.augmentcode.com/cli/integrations)
- [Augment MCP setup](https://docs.augmentcode.com/setup-augment/mcp)
- [Augment Code Review MCP context](https://docs.augmentcode.com/codereview/mcp-context)
- [Auggie Agent Skills](https://docs.augmentcode.com/cli/skills)
- [npx skills](https://github.com/vercel-labs/skills)
