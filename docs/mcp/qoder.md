# Qoder

<!-- Generated from Entalpa's canonical integration source. -->

Use Qoder's local CLI or IDE runtime for Entalpa, then install the skills with the verified `npx skills` Qoder target or Qoder's native skills paths.

## Requirements

- Qoder CLI or IDE with its local runtime and MCP support.
- Browser access for OAuth.

## Install MCP Server

### Add with Qoder CLI

```bash
qodercli mcp add -t http -s user entalpa https://api.entalpa.com/mcp
```

### Qoder IDE UI path

Open Qoder Settings, select MCP, add a server on the My Servers tab, and use `https://api.entalpa.com/mcp`. Qoder IDE can auto-detect Streamable HTTP when configured through the remote/SSE endpoint flow.

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
npx skills add entalpa/entalpa-mcp --skill "*" --agent qoder -g -y
```

### Manual user skills fallback

```bash
tmpdir="$(mktemp -d)"
git clone --depth 1 https://github.com/entalpa/entalpa-mcp.git "$tmpdir"
mkdir -p ~/.qoder/skills
cp -R "$tmpdir/skills/." ~/.qoder/skills/
```

### Project skills alternative

```bash
tmpdir="$(mktemp -d)"
git clone --depth 1 https://github.com/entalpa/entalpa-mcp.git "$tmpdir"
mkdir -p .qoder/skills
cp -R "$tmpdir/skills/." .qoder/skills/
```

## Verify

- Run `qodercli mcp list` or reload MCP servers with `/mcp reload`.
- In Qoder Agent mode, ask it to list Entalpa projects and approve the MCP tool call.
- Restart Qoder and type `/` to confirm both Entalpa skills are discoverable.

## Known Limitations

- This direct Entalpa setup is local-runtime only. Qoder CLI Cloud Mode runs on a managed cloud VM and does not use the local MCP configuration.
- Qoder's experimental Cloud Agent rejects `mcpServers` and does not support MCP OAuth. Do not reuse this direct path for cloud-agent sessions.

## Sources

- [Qoder CLI MCP servers](https://docs.qoder.com/en/cli/mcp-servers)
- [Qoder MCP settings](https://docs.qoder.com/user-guide/chat/model-context-protocol)
- [Qoder Cloud Agent constraints](https://docs.qoder.com/en/cli/sdk/cloud-agent)
- [Qoder Cloud Mode](https://docs.qoder.com/en/cli/cloud-mode)
- [Qoder skills](https://docs.qoder.com/extensions/skills)
- [npx skills](https://github.com/vercel-labs/skills)
