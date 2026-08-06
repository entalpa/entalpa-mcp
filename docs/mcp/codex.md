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

### Add the plugin marketplace from the CLI

```bash
codex plugin marketplace add entalpa/entalpa-mcp --sparse .agents/plugins --sparse plugins
```

### Install the plugin from the CLI

```bash
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

- Start Codex and ask it to use Entalpa to list projects.
- Check `~/.codex/config.toml` if the server does not appear.

## Known Limitations

- The marketplace command works after the public repository contains `.agents/plugins/marketplace.json` and the bundled plugin directory. Use `/plugins` as the UI alternative.

## Sources

- [Codex MCP](https://learn.chatgpt.com/docs/extend/mcp)
- [Codex Plugins](https://learn.chatgpt.com/docs/plugins)
- [Build Codex plugins](https://developers.openai.com/plugins/build/plugins)
- [Codex Skills](https://learn.chatgpt.com/docs/build-skills)
- [npx skills](https://github.com/vercel-labs/skills)
- [GitHub CLI skills](https://cli.github.com/manual/gh_skill)
