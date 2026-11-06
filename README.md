# Entalpa MCP: spec-driven development for AI coding agents

<!-- Generated from Entalpa's canonical integration source. -->

Entalpa is a spec-driven development platform for AI coding agents: a persistent, MCP-native specification layer (stakeholders, needs, user stories, requirements, design) with atomic locking and open questions surfaced before the build, for people building with Claude Code, Cursor and Codex. Learn more at [entalpa.com](https://entalpa.com).

This repository connects supported AI clients to Entalpa's remote MCP server and installs its portable Agent Skills: `entalpa-implement`, `entalpa-prd`, `entalpa-openspec`, `entalpa-speckit`. The agent reads the spec before it writes code, records which requirements it implemented and tested, and asks before changing a locked requirement.

Entalpa is not a workflow and does not replace Spec Kit, OpenSpec or your `CLAUDE.md`/`AGENTS.md`: those decide how the agent works, the spec holds what the product must do, and they compose. The `entalpa-speckit` and `entalpa-openspec` skills keep an Entalpa project in step with a Spec Kit or OpenSpec repository.

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

The bundled plugin installs the Entalpa MCP connection and every published skill together in clients with plugin support.

### Claude: claude.ai, the desktop app and Cowork

Entalpa is listed in Claude's plugin directory. Open [Customize > Plugins](https://claude.ai/customize/plugins), search for Entalpa on the **Discover** tab, and select **Add**. Then open the plugin's **Connectors** tab and connect `entalpa`. The plugin is saved to your Claude account, so it also loads in Cowork and in Claude Code. On Team and Enterprise plans, an Owner may first have to make the directory's plugins available and add the connector for the organization.

The Entalpa connector is listed in the [Connectors directory](https://claude.ai/directory/entalpa) too. Connect it there to use the server without the plugin, for example on a Free plan, where the directory's plugins are not available, and upload the skills from `skills/` yourself.

### Claude Code

Install the plugin from Claude's plugin directory (Claude Code 2.1.287 or later; `/plugin directory entalpa` finds it from a session):

```bash
claude plugin install entalpa@anthropic-plugin-directory
```

If you added Entalpa on claude.ai, Claude Code 2.1.273 or later already loads it as `entalpa@synced` in sessions signed in with that Claude account; install it one way only. On older versions, or where your organization blocks the directory, use the repository marketplace:

```bash
claude plugin marketplace add entalpa/entalpa-mcp --sparse .claude-plugin plugins
claude plugin install entalpa@entalpa-plugins
```

Then run `/mcp`, select `plugin:entalpa:entalpa`, and sign in to Entalpa.

### Codex

```bash
codex plugin marketplace add entalpa/entalpa-mcp --sparse .agents/plugins --sparse plugins
codex plugin add entalpa@entalpa-plugins
```

Alternatively, after adding the marketplace, open `/plugins`, select the Entalpa Plugins marketplace, and install `entalpa` there. Adding a marketplace only registers its catalog; the plugin installation is what enables the bundled MCP server and skills.

## Repository Layout

- `skills/entalpa-implement/`: Entalpa Implement.
- `skills/entalpa-prd/`: Entalpa PRD.
- `skills/entalpa-openspec/`: Entalpa for OpenSpec.
- `skills/entalpa-speckit/`: Entalpa for Spec Kit.
- `plugins/entalpa/`: self-contained Codex, Claude Code and Cursor plugin bundle containing every skill above.
- `docs/mcp/`: client-specific installation and troubleshooting guides.

## Versions and Changes

Released versions and what changed in each are in [CHANGELOG.md](CHANGELOG.md). For reproducible, tag-pinned install commands see [docs/mcp/release-and-versioning.md](docs/mcp/release-and-versioning.md).

## Support and Policies

- MCP setup and support: https://entalpa.com/en/connect
- Email: contact@entalpa.com
- Privacy policy: https://entalpa.com/en/privacy-policy
- Terms of service: https://entalpa.com/en/terms-of-service

## License

MIT. See [LICENSE](LICENSE).
