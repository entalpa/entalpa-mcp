# Qoder CN and QoderWork CN

<!-- Generated from Entalpa's canonical integration source. -->

Use this regional guide for Qoder CN, formerly Tongyi Lingma, and QoderWork CN. Qoder CN requires a compatible hosted or bridged MCP route because its documented direct transports do not provide Entalpa's OAuth flow.

## Requirements

- Qoder CN, formerly Tongyi Lingma, plugin version 2.5.0 or later, or QoderWork CN.
- Agent mode enabled with a supported Qwen model.
- A ModelScope-hosted Entalpa service, a tested compatible bridge, or a QoderWork CN build whose remote OAuth behavior has been validated.

## Install MCP Server

### Add through MCP service settings

Open the avatar menu, choose Personal Settings, then MCP Service. Add a service named `entalpa` manually or through the configuration-file option.

### ModelScope or SSE bridge path

Qoder CN docs currently document STDIO and SSE examples. Use ModelScope MCP Plaza, or an Entalpa-compatible SSE bridge URL, only after Entalpa has a compatible ModelScope-hosted MCP entry or tested bridge.

### QoderWork CN Streamable HTTP path

```json
{
  "mcpServers": {
    "entalpa": {
      "type": "streamable-http",
      "url": "https://api.entalpa.com/mcp"
    }
  }
}
```

## Install Entalpa Skill

Install from `entalpa/entalpa-mcp`'s default branch for the latest skill, or use a release tag for a reproducible install.

### Install the Entalpa skills for Qoder CN

```bash
npx skills add entalpa/entalpa-mcp --skill "*" --agent lingma -g -y
```

### Manual user skills fallback

```bash
tmpdir="$(mktemp -d)"
git clone --depth 1 https://github.com/entalpa/entalpa-mcp.git "$tmpdir"
mkdir -p ~/.lingma/skills
cp -R "$tmpdir/skills/." ~/.lingma/skills/
```

### Project skills alternative

```bash
tmpdir="$(mktemp -d)"
git clone --depth 1 https://github.com/entalpa/entalpa-mcp.git "$tmpdir"
mkdir -p .lingma/skills
cp -R "$tmpdir/skills/." .lingma/skills/
```

### Built-in creator fallback

If manual import is not available, use Qoder CN's built-in skill creation flow with both Entalpa `SKILL.md` instruction files.

## Verify

- Confirm the MCP service shows a connected state and lists Entalpa tools.
- Switch the chat to Agent mode before asking Qoder CN to list Entalpa projects.
- Restart the IDE and type `/` to verify both Entalpa skills are visible.

## Known Limitations

- Official Qoder CN docs emphasize STDIO and SSE and do not document direct remote MCP OAuth. Do not point an SSE config at Entalpa's Streamable HTTP `/mcp` endpoint or claim direct OAuth support.
- QoderWork CN Streamable HTTP support is documented separately from Qoder CN IDE behavior; its Entalpa OAuth flow remains untested and must be validated before sharing a team config.

## Sources

- [Qoder CN product overview](https://help.aliyun.com/zh/lingma)
- [Tongyi Lingma Qoder CN MCP](https://help.aliyun.com/zh/lingma/qoder-cn/user-guide/guide-for-using-mcp)
- [Tongyi Lingma April 2025 product updates](https://help.aliyun.com/en/lingma/product-overview/changelogs-of-202504)
- [ModelScope MCP Lingma integration](https://modelscope.cn/docs/mcp/lingma)
- [ModelScope MCP Plaza](https://modelscope.cn/mcp)
- [QoderWork CN MCP](https://help.aliyun.com/en/lingma/qoderwork-cn/mcp)
- [Tongyi Lingma Qoder CN skills](https://help.aliyun.com/zh/lingma/qoder-cn/user-guide/skills)
- [npx skills](https://github.com/vercel-labs/skills)
