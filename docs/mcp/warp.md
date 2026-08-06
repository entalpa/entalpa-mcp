# Warp

<!-- Generated from Entalpa's canonical integration source. -->

Use Warp's desktop MCP settings to complete Entalpa browser OAuth, then reuse the validated configuration in supported local or Oz agent runs.

## Requirements

- Warp with Agent Mode and MCP support.
- Browser access for OAuth.

## Install MCP Server

### Add through Warp MCP settings

Open Settings, MCP Servers (also available from Settings, AI, Manage MCP servers), then add a Streamable HTTP server named `entalpa` with URL `https://api.entalpa.com/mcp`.

### Authenticate locally

Start a local Warp Agent session, select the Entalpa MCP server, and complete the browser OAuth flow when Warp prompts.

### Alternate local access paths

Warp also exposes local MCP server management through Warp Drive and the Command Palette.

### Oz CLI path after desktop authentication

Oz accepts MCP configuration through `--mcp` for local and cloud runs. Warp has added reuse of previously authenticated OAuth MCP servers for local CLI agent runs; validate cloud reuse separately before automation.

## Install Entalpa Skill

Install from `entalpa/entalpa-mcp`'s default branch for the latest skill, or use a release tag for a reproducible install.

### Install the Entalpa skills

```bash
npx skills add entalpa/entalpa-mcp --skill "*" --agent warp -g -y
```

## Verify

- Ask Warp Agent to list Entalpa projects.

## Known Limitations

- Oz accepts MCP configuration for `oz agent run` and `oz agent run-cloud`. Warp documents reuse of previously authenticated OAuth servers for local CLI agent runs; cloud reuse remains runtime-unverified, so authenticate in the desktop app first and test the exact execution surface before relying on it.
- Entalpa OAuth remains runtime-unverified in Warp's local agent; keep this limitation until tested end to end.

## Sources

- [Warp MCP](https://docs.warp.dev/agents/capabilities/mcp/)
- [Warp MCP workflows](https://docs.warp.dev/guides/external-tools/using-mcp-servers-with-warp/)
- [Warp MCP servers for cloud agents](https://docs.warp.dev/platform/mcp/)
- [Warp changelog](https://docs.warp.dev/changelog)
- [Warp Agent Skills](https://docs.warp.dev/agents/capabilities/skills/)
- [npx skills](https://github.com/vercel-labs/skills)
