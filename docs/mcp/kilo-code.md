# Kilo Code

<!-- Generated from Entalpa's canonical integration source. -->

Add Entalpa as a remote MCP server in Kilo Code or `kilo.jsonc`, then install the Entalpa skills through Kilo's native skill directories or compatibility paths.

## Requirements

- Kilo Code extension or Kilo CLI installed.
- Browser access for OAuth if Kilo starts the Entalpa authorization flow.

## Install MCP Server

### Add through Kilo Code settings

In the Kilo Code extension, open Settings, Agent Behaviour, MCP Servers, then add a Remote HTTP server named `entalpa` with URL `https://api.entalpa.com/mcp`.

### Global or project config

```json
{
  "mcp": {
    "entalpa": {
      "type": "remote",
      "url": "https://api.entalpa.com/mcp",
      "enabled": true,
      "timeout": 15000
    }
  }
}
```

## Install Entalpa Skill

Install from `entalpa/entalpa-mcp`'s default branch for the latest skill, or use a release tag for a reproducible install.

### Install as Kilo user skills

```bash
tmpdir="$(mktemp -d)"
git clone --depth 1 https://github.com/entalpa/entalpa-mcp.git "$tmpdir"
mkdir -p ~/.kilo/skills
cp -R "$tmpdir/skills/." ~/.kilo/skills/
```

### Project skills alternative

```bash
tmpdir="$(mktemp -d)"
git clone --depth 1 https://github.com/entalpa/entalpa-mcp.git "$tmpdir"
mkdir -p .kilo/skills
cp -R "$tmpdir/skills/." .kilo/skills/
```

### Compatibility path alternative

```bash
tmpdir="$(mktemp -d)"
git clone --depth 1 https://github.com/entalpa/entalpa-mcp.git "$tmpdir"
mkdir -p .agents/skills
cp -R "$tmpdir/skills/." .agents/skills/
```

### Skills CLI status

Do not use `npx skills --agent kilo` as the primary Kilo Code path until the Skills CLI target maps to Kilo's documented `.kilo/skills` paths instead of `.kilocode/skills`.

## Verify

- Confirm Kilo Code shows Entalpa as a connected MCP server.
- Ask Kilo Code to list Entalpa projects and approve OAuth/tool calls when prompted.
- Start a new session and ask Kilo Code what skills are available.

## Known Limitations

- Kilo supports Remote HTTP / Streamable HTTP and documents SSE as deprecated. Verify Entalpa OAuth behavior in the installed Kilo version.
- The current Skills CLI `kilo` target writes `.kilocode/skills`, while Kilo's official docs use `.kilo/skills`.
- Kilo's marketplace is currently a GitHub repository; direct submission should be handled after the generated docs are reviewed.

## Sources

- [Kilo Code MCP](https://kilo.ai/docs/automate/mcp/using-in-kilo-code)
- [Kilo Code skills](https://kilo.ai/docs/customize/skills)
- [Kilo Marketplace](https://github.com/Kilo-Org/kilo-marketplace)
- [npx skills](https://github.com/vercel-labs/skills)
