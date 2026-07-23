# OpenClaw

<!-- Generated from Entalpa's canonical integration source. -->

Save Entalpa as an OpenClaw-managed Streamable HTTP MCP server with OAuth, then install the Entalpa skills from the local skill directories until ClawHub listings exist.

## Requirements

- OpenClaw installed and configured.
- Browser access for OpenClaw's OAuth authorization URL.
- An OpenClaw runtime that projects saved MCP servers into the target agent profile.

## Install MCP Server

### Add the MCP server

```bash
openclaw mcp add entalpa --url https://api.entalpa.com/mcp --transport streamable-http --auth oauth
```

### Start OAuth login

```bash
openclaw mcp login entalpa
```

### Finish OAuth login

OpenClaw prints an authorization URL. Approve it in the browser, then rerun `openclaw mcp login entalpa --code <returned-code>` if the flow requires pasting the code.

### Probe the server

```bash
openclaw mcp doctor entalpa --probe
```

### Control UI alternative

Open the OpenClaw Control UI and use the MCP page at `/mcp` to review or edit the same `mcp` configuration.

## Install Entalpa Skill

Install from `entalpa/entalpa-mcp`'s default branch for the latest skill, or use a release tag for a reproducible install.

### Install both Entalpa skills

```bash
tmpdir="$(mktemp -d)"
git clone --depth 1 https://github.com/entalpa/entalpa-mcp.git "$tmpdir"
openclaw skills install "$tmpdir/skills/entalpa-implement" --as entalpa-implement
openclaw skills install "$tmpdir/skills/entalpa-prd" --as entalpa-prd
```

### Future ClawHub path

After publishing both skills to ClawHub, install and verify `@entalpa/entalpa-implement` and `@entalpa/entalpa-prd` separately.

### Skills CLI alternative

```bash
npx skills add entalpa/entalpa-mcp --skill "*" --agent openclaw -g -y
```

## Verify

- Run `openclaw mcp status --verbose` or `openclaw mcp show entalpa --json` and confirm OAuth/token status is healthy.
- Run `openclaw mcp probe entalpa --json` and confirm Entalpa tools are listed.
- Start a new OpenClaw agent session and confirm both Entalpa skills are in the effective skill list.

## Known Limitations

- `openclaw mcp add` saves definitions for runtimes OpenClaw manages later; it does not expose Entalpa tools in every external client automatically.
- OpenClaw Git skill installs expect `SKILL.md` at the source root, so use the local directory install until Entalpa has a ClawHub slug or root-level skill package.

## Sources

- [OpenClaw MCP](https://docs.openclaw.ai/cli/mcp)
- [OpenClaw skills](https://docs.openclaw.ai/tools/skills)
- [ClawHub](https://docs.openclaw.ai/clawhub)
- [npx skills](https://github.com/vercel-labs/skills)
