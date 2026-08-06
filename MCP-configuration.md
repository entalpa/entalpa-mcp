# Entalpa MCP Configuration

<!-- Generated from Entalpa's canonical integration source. -->

Entalpa provides a remote Model Context Protocol server for live requirements engineering context.

- MCP URL: `https://api.entalpa.com/mcp`
- Transport: `streamable-http`
- Authentication: OAuth through Entalpa/Keycloak
- Skills: `entalpa-implement`, `entalpa-prd`

## Recommended Installs

| Client | Preferred MCP install | Skill path | Guide |
|---|---|---|---|
| Claude Code | `claude mcp add --transport http entalpa https://api.entalpa.com/mcp` | Plugin install includes MCP + skills | [Guide](docs/mcp/claude-code.md) |
| Claude Desktop and Claude.ai | In Free, Pro, or Max, open Customize, choose Connectors, then add a custom connector. Free accounts are limited to one custom connector. In Team or Enterprise plans, an Owner or Primary Owner adds custom connectors from Organization settings before members connect from Customize, Connectors. | Create one ZIP per canonical skill directory, with the corresponding `entalpa-implement` or `entalpa-prd` folder from `skills/` at the archive root. | [Guide](docs/mcp/claude-desktop.md) |
| Codex CLI, IDE, and App | `codex mcp add entalpa --url https://api.entalpa.com/mcp` | `codex plugin marketplace add entalpa/entalpa-mcp --sparse .agents/plugins --sparse plugins` | [Guide](docs/mcp/codex.md) |
| ChatGPT and OpenAI API | Developer mode is a one-time switch that lets ChatGPT talk to outside apps like Entalpa. On Pro, open Settings, then Apps, then Advanced settings, and turn it on. On Business, Enterprise, or Edu, an admin or owner turns it on (Enterprise and Edu admins may first grant you access under Permissions and roles). | You only need these for the guided implementation and PRD/BRD workflows; they are not required for fetching a project or writing reports. In the ChatGPT sidebar, open Plugins, select the Skills tab, choose Create, then Upload from your computer, and upload the packaged `entalpa-implement` and `entalpa-prd` skills one at a time. ChatGPT, Codex, and API skills are stored separately. | [Guide](docs/mcp/chatgpt-and-openai-api.md) |
| Cursor | Native UI or config | `npx skills add entalpa/entalpa-mcp --skill "*" --agent cursor -g -y` | [Guide](docs/mcp/cursor.md) |
| VS Code and GitHub Copilot | Native UI or config | `copilot plugin marketplace add entalpa/entalpa-mcp && copilot plugin install entalpa@entalpa-plugins` | [Guide](docs/mcp/vscode-github-copilot.md) |
| GitHub Copilot CLI | `copilot mcp add entalpa --type http --url https://api.entalpa.com/mcp` | `copilot plugin marketplace add entalpa/entalpa-mcp && copilot plugin install entalpa@entalpa-plugins` | [Guide](docs/mcp/github-copilot-cli.md) |
| Devin Desktop and Cascade | Use the Cascade `MCPs` icon or open Devin Settings, Cascade, MCP Servers. Add a remote HTTP server when prompted. | Manual skill install; see guide | [Guide](docs/mcp/windsurf.md) |
| Kiro | Native UI or config | `npx skills add entalpa/entalpa-mcp --skill "*" --agent kiro-cli -g -y` | [Guide](docs/mcp/kiro.md) |
| OpenCode | `opencode mcp add` | `npx skills add entalpa/entalpa-mcp --skill "*" --agent opencode -g -y` | [Guide](docs/mcp/opencode.md) |
| Goose | `goose configure` | `npx skills add entalpa/entalpa-mcp --skill "*" --agent goose -g -y` | [Guide](docs/mcp/goose.md) |
| Trae | Native UI or config | `npx skills add entalpa/entalpa-mcp --skill "*" --agent trae -g -y` | [Guide](docs/mcp/trae.md) |
| Qwen Code | `qwen mcp add -s user -t http entalpa https://api.entalpa.com/mcp` | `npx skills add entalpa/entalpa-mcp --skill "*" --agent qwen-code -g -y` | [Guide](docs/mcp/qwen-code.md) |
| Qoder | `qodercli mcp add -t http -s user entalpa https://api.entalpa.com/mcp` | `npx skills add entalpa/entalpa-mcp --skill "*" --agent qoder -g -y` | [Guide](docs/mcp/qoder.md) |
| Qoder CN and QoderWork CN | Native UI or config | `npx skills add entalpa/entalpa-mcp --skill "*" --agent lingma -g -y` | [Guide](docs/mcp/tongyi-lingma-qoder-cn.md) |
| Tencent CodeBuddy | `codebuddy mcp add --scope user --transport http entalpa https://api.entalpa.com/mcp` | `npx skills add entalpa/entalpa-mcp --skill "*" --agent codebuddy -g -y` | [Guide](docs/mcp/codebuddy.md) |

## Fast Paths

Claude Code:

```bash
claude mcp add --transport http entalpa https://api.entalpa.com/mcp
```

Codex:

```bash
codex mcp add entalpa --url https://api.entalpa.com/mcp
codex mcp login entalpa
```

Generic fallback for supported coding agents:

```bash
npx add-mcp https://api.entalpa.com/mcp --name entalpa --transport http
```

## Generic MCP Configuration

Use this only when your MCP client does not have a native installer, and verify the exact field names in that client's documentation. Generic MCP JSON shapes are not portable across all Streamable HTTP clients.

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

Some clients use `httpUrl`, `streamableHttp`, or `servers` instead of this shape. Prefer the client-specific guide when one exists.

## Skill Installation

The Entalpa skills teach coding agents how to work with requirements and traceability, including implementation and grounded PRD/BRD generation.

The commands below install from `entalpa/entalpa-mcp`'s default branch. Use a release tag when you need a reproducible version.

```bash
npx skills add entalpa/entalpa-mcp --skill "*" --agent codex -g -y
gh skill install entalpa/entalpa-mcp entalpa-implement --agent codex --scope user
gh skill install entalpa/entalpa-mcp entalpa-prd --agent codex --scope user
```

`npx skills` installs every published Entalpa skill in one command. GitHub CLI installs each named skill separately. Change `codex` to your target agent when supported by the installer.

## Client Guides

- [Claude Code](docs/mcp/claude-code.md)
- [Claude Desktop and Claude.ai](docs/mcp/claude-desktop.md)
- [Codex CLI, IDE, and App](docs/mcp/codex.md)
- [ChatGPT and OpenAI API](docs/mcp/chatgpt-and-openai-api.md)
- [Cursor](docs/mcp/cursor.md)
- [VS Code and GitHub Copilot](docs/mcp/vscode-github-copilot.md)
- [GitHub Copilot CLI](docs/mcp/github-copilot-cli.md)
- [Devin Desktop and Cascade](docs/mcp/windsurf.md)
- [Kiro](docs/mcp/kiro.md)
- [OpenCode](docs/mcp/opencode.md)
- [Goose](docs/mcp/goose.md)
- [Trae](docs/mcp/trae.md)
- [Qwen Code](docs/mcp/qwen-code.md)
- [Qoder](docs/mcp/qoder.md)
- [Qoder CN and QoderWork CN](docs/mcp/tongyi-lingma-qoder-cn.md)
- [Tencent CodeBuddy](docs/mcp/codebuddy.md)
- [Google Antigravity](docs/mcp/antigravity.md)
- [Gemini CLI](docs/mcp/gemini-cli.md)
- [Amp](docs/mcp/amp.md)
- [Amazon Q Developer for Existing IDE Customers](docs/mcp/amazon-q.md)
- [Android Studio Gemini](docs/mcp/android-studio.md)
- [Augment Code](docs/mcp/augment.md)
- [Cline](docs/mcp/cline.md)
- [Continue](docs/mcp/continue.md)
- [Devin](docs/mcp/devin.md)
- [Docker MCP Catalog and Toolkit](docs/mcp/docker-mcp-toolkit.md)
- [JetBrains AI Assistant](docs/mcp/jetbrains-ai-assistant.md)
- [Replit](docs/mcp/replit.md)
- [Kimi Playground](docs/mcp/kimi-playground.md)
- [OpenClaw](docs/mcp/openclaw.md)
- [Kilo Code](docs/mcp/kilo-code.md)
- [Roo Code](docs/mcp/roo-code.md)
- [Warp](docs/mcp/warp.md)
- [Zed](docs/mcp/zed.md)
- [Generic MCP clients](docs/mcp/generic-mcp-clients.md)
- [Plugins and registries](docs/mcp/plugins-and-registries.md)
- [Release and versioning](docs/mcp/release-and-versioning.md)
- [Troubleshooting](docs/mcp/troubleshooting.md)
- [Sources](docs/mcp/sources.md)

## Discovery and Registries

Use the client-specific installers and plugin bundles documented here. Registry and directory links should be advertised only after their listings are published and verified.

## Troubleshooting

See [docs/mcp/troubleshooting.md](docs/mcp/troubleshooting.md).

## Sources

- [Claude Code MCP](https://code.claude.com/docs/en/mcp)
- [Codex MCP](https://learn.chatgpt.com/docs/extend/mcp)
- [Connect MCP servers from ChatGPT](https://developers.openai.com/apps-sdk/deploy/connect-chatgpt)
- [add-mcp](https://github.com/neon-solutions/add-mcp)
- [npx skills](https://github.com/vercel-labs/skills)
- [MCP Registry](https://modelcontextprotocol.io/registry/about)
