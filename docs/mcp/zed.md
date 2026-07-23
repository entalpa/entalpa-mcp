# Zed

<!-- Generated from Entalpa's canonical integration source. -->

Configure Entalpa as a Zed custom remote MCP server with `context_servers`, then install the skills in Zed's documented skills path.

## Requirements

- Current stable Zed build with MCP support.
- Browser access for OAuth.

## Install MCP Server

### Add through Zed settings

Open Settings, AI, MCP Servers, choose Add Server, then Add Remote Server. Name it `entalpa`, use `https://api.entalpa.com/mcp`, and leave the Authorization header unset so Zed starts standard MCP OAuth.

### Direct remote MCP config

```json
{
  "context_servers": {
    "entalpa": {
      "url": "https://api.entalpa.com/mcp"
    }
  }
}
```

## Install Entalpa Skill

Install from `entalpa/entalpa-mcp`'s default branch for the latest skill, or use a release tag for a reproducible install.

### Install the Entalpa skills manually

```bash
tmpdir="$(mktemp -d)"
git clone --depth 1 https://github.com/entalpa/entalpa-mcp.git "$tmpdir"
mkdir -p .agents/skills
cp -R "$tmpdir/skills/." .agents/skills/
```

## Verify

- Open the Zed Agent Panel and confirm the Entalpa MCP server status.
- If Zed prompts for OAuth because no Authorization header is configured, complete the browser authorization flow.

## Known Limitations

- Validate Entalpa OAuth behavior against the installed Zed build before sharing this as a team standard.
- Do not document a bridge until it is tested against the current stable Zed build.

## Sources

- [Zed MCP](https://zed.dev/docs/ai/mcp)
- [Zed skills](https://zed.dev/docs/ai/skills)
