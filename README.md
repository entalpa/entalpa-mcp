# Entalpa Integrations

<!-- Generated from Entalpa's canonical integration source. -->

Connect supported AI clients to Entalpa's remote MCP server and install its portable Agent Skills: `entalpa-implement`, `entalpa-prd`.

## Install the Skills

```bash
npx skills add entalpa/entalpa-mcp
```

The interactive installer discovers all Entalpa skills and lets you select them. For a deterministic global installation of every skill into a supported client, use:

```bash
npx skills add entalpa/entalpa-mcp --skill "*" --agent <agent> -g -y
```

## Connect the MCP Server

- URL: `https://api.entalpa.com/mcp`
- Transport: Streamable HTTP
- Authentication: OAuth through Entalpa

See [MCP-configuration.md](MCP-configuration.md) for native client installers, configuration examples, and compatibility notes.

## Plugin Installation

The bundled plugin installs the Entalpa MCP connection and every published skill together in clients with plugin marketplace support.

### Codex

```bash
codex plugin marketplace add entalpa/entalpa-mcp --sparse .agents/plugins --sparse plugins
```

Open `/plugins`, select the Entalpa Plugins marketplace, and install `entalpa`.

### Claude Code

```bash
claude plugin marketplace add entalpa/entalpa-mcp --sparse .claude-plugin plugins
claude plugin install entalpa@entalpa-plugins
```

## Repository Layout

- `skills/entalpa-implement/`: Entalpa Implement.
- `skills/entalpa-prd/`: Entalpa PRD.
- `plugins/entalpa/`: self-contained Codex and Claude Code plugin bundle containing every skill above.
- `docs/mcp/`: client-specific installation and troubleshooting guides.

## License

MIT. See [LICENSE](LICENSE).
