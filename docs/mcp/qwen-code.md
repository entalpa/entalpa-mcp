# Qwen Code

<!-- Generated from Entalpa's canonical integration source. -->

Use Qwen Code's native `qwen mcp add` HTTP transport for the Entalpa MCP server, then install the Entalpa skills into Qwen's user or project skills directory.

## Requirements

- Qwen Code installed and signed in.
- Browser access for the OAuth flow; remote/cloud terminal users may need a custom OAuth redirect URI.

## Install MCP Server

### Add the MCP server

```bash
qwen mcp add -s user -t http entalpa https://api.entalpa.com/mcp
```

### Manual settings fallback

```json
{
  "mcpServers": {
    "entalpa": {
      "httpUrl": "https://api.entalpa.com/mcp",
      "timeout": 30000,
      "oauth": {
        "redirectUri": "http://localhost:7777/oauth/callback"
      }
    }
  }
}
```

### Authenticate when prompted

Qwen Code supports OAuth discovery for remote HTTP MCP servers. If the browser flow does not start automatically, open `/mcp`, select `entalpa`, and use the reconnect or authorization action shown by Qwen Code. The server-specific JSON key is `mcpServers.entalpa.oauth.redirectUri`; remote or cloud terminals must replace the localhost default with a publicly reachable callback and may set the same value with `--oauth-redirect-uri`.

## Install Entalpa Skill

Install from `entalpa/entalpa-mcp`'s default branch for the latest skill, or use a release tag for a reproducible install.

### Install the Entalpa skills with Skills CLI

```bash
npx skills add entalpa/entalpa-mcp --skill "*" --agent qwen-code -g -y
```

### Manual user skills fallback

```bash
tmpdir="$(mktemp -d)"
git clone --depth 1 https://github.com/entalpa/entalpa-mcp.git "$tmpdir"
mkdir -p ~/.qwen/skills
cp -R "$tmpdir/skills/." ~/.qwen/skills/
```

### Project skills alternative

```bash
tmpdir="$(mktemp -d)"
git clone --depth 1 https://github.com/entalpa/entalpa-mcp.git "$tmpdir"
mkdir -p .qwen/skills
cp -R "$tmpdir/skills/." .qwen/skills/
```

## Verify

- Run Qwen Code and use `/mcp` to confirm Entalpa is connected and tools are listed.
- If authentication is pending, open `/mcp`, select `entalpa`, and use the reconnect or authorization action shown by Qwen Code.
- Ask Qwen Code what skills are available and confirm `entalpa-implement` and `entalpa-prd` are listed.

## Known Limitations

- Use `httpUrl` or `-t http` for Streamable HTTP. Qwen's `url` field is for SSE.

## Sources

- [Qwen Code MCP servers](https://qwenlm.github.io/qwen-code-docs/en/developers/tools/mcp-server/)
- [Qwen Code agent skills](https://qwenlm.github.io/qwen-code-docs/en/users/features/skills/)
- [npx skills](https://github.com/vercel-labs/skills)
