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
- Account: an Entalpa account is required. Your client opens Entalpa's sign-in on first connect and registers itself; there is no API key to paste. Create an account at [entalpa.com](https://entalpa.com).

The server reads and writes the projects that account can already see. The skills below are what tell an agent how to use it well, but the connection works without them.

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

## Versions and Changes

Released versions and what changed in each are in [CHANGELOG.md](CHANGELOG.md). For reproducible, tag-pinned install commands see [docs/mcp/release-and-versioning.md](docs/mcp/release-and-versioning.md).

## Support and Policies

- MCP setup and support: https://entalpa.com/en/connect-mcp
- Email: contact@entalpa.com
- Privacy policy: https://entalpa.com/en/privacy-policy
- Terms of service: https://entalpa.com/en/terms-of-service

## License

MIT. See [LICENSE](LICENSE).
