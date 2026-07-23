# Devin Desktop and Cascade

<!-- Generated from Entalpa's canonical integration source. -->

Use Devin Desktop's Cascade MCP UI for remote Streamable HTTP, then commit the Entalpa skills to a native repository skills path.

## Requirements

- Devin Desktop with Cascade MCP support.
- Browser access for OAuth.

## Install MCP Server

### Add through Cascade MCP settings

Use the Cascade `MCPs` icon or open Devin Settings, Cascade, MCP Servers. Add a remote HTTP server when prompted.

### Configure Entalpa

Name the server `entalpa` and use URL `https://api.entalpa.com/mcp`.

## Install Entalpa Skill

Install from `entalpa/entalpa-mcp`'s default branch for the latest skill, or use a release tag for a reproducible install.

### Install as native repository skills

```bash
tmpdir="$(mktemp -d)"
git clone --depth 1 https://github.com/entalpa/entalpa-mcp.git "$tmpdir"
mkdir -p .agents/skills
cp -R "$tmpdir/skills/." .agents/skills/
```

### Historical Skills CLI alternative

```bash
npx skills add entalpa/entalpa-mcp --skill "*" --agent windsurf -g -y
```

## Verify

- Restart Cascade and confirm Entalpa tools are listed.

## Known Limitations

- Prefer the UI because raw config paths and keys are more likely to change.
- Devin recommends repository-scoped `.agents/skills`; `.windsurf/skills` is also discovered. The portable Skills CLI still uses the historical `windsurf` identifier, so keep it as a compatibility alternative.

## Sources

- [Windsurf Cascade MCP](https://docs.devin.ai/desktop/cascade/mcp)
- [Devin product skills](https://docs.devin.ai/product-guides/skills)
- [npx skills](https://github.com/vercel-labs/skills)
