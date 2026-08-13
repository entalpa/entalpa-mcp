# Codex CLI, IDE, and App

<!-- Generated from Entalpa's canonical integration source. -->

Use the Entalpa Codex plugin to install MCP plus all skills together, or use Codex's native MCP command and `npx skills` when you want separate setup.

## Requirements

- Codex CLI installed and signed in.
- Browser access for OAuth login.

## Install MCP Server

### Add the MCP server

```bash
codex mcp add entalpa --url https://api.entalpa.com/mcp
```

### Authenticate with OAuth

```bash
codex mcp login entalpa
```

## Install Entalpa Skill

Install from `entalpa/entalpa-mcp`'s default branch for the latest skill, or use a release tag for a reproducible install.

### Preferred plugin path

```bash
codex plugin marketplace add entalpa/entalpa-mcp --sparse .agents/plugins --sparse plugins
codex plugin add entalpa@entalpa-plugins
```

### Codex UI alternative

Open `/plugins` in Codex, choose the Entalpa Plugins marketplace, then install and enable `entalpa`.

### Install the Entalpa skills

```bash
npx skills add entalpa/entalpa-mcp --skill "*" --agent codex -g -y
```

### GitHub CLI alternative

```bash
gh skill install entalpa/entalpa-mcp entalpa-implement --agent codex --scope user
gh skill install entalpa/entalpa-mcp entalpa-prd --agent codex --scope user
```

## Verify

- Run `codex mcp get entalpa --json` after plugin installation and confirm that it reports `https://api.entalpa.com/mcp` as enabled.
- Start Codex and ask it to use Entalpa to list projects.

## Known Limitations

- `codex plugin marketplace add` registers a catalog but does not install its plugins. Follow it with `codex plugin add entalpa@entalpa-plugins` or install `entalpa` from `/plugins`.

## Sources

- [Codex MCP](https://learn.chatgpt.com/docs/extend/mcp)
- [Codex Plugins](https://learn.chatgpt.com/docs/plugins)
- [Build Codex plugins](https://developers.openai.com/plugins/build/plugins)
- [Codex 0.147.0 plugin MCP parser](https://github.com/openai/codex/blob/rust-v0.147.0/codex-rs/codex-mcp/src/plugin_config.rs#L35-L50)
- [Codex Skills](https://learn.chatgpt.com/docs/build-skills)
- [npx skills](https://github.com/vercel-labs/skills)
- [GitHub CLI skills](https://cli.github.com/manual/gh_skill)
