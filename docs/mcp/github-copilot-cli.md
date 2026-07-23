# GitHub Copilot CLI

<!-- Generated from Entalpa's canonical integration source. -->

Prefer the Entalpa Copilot plugin to install MCP plus all skills together, or use Copilot CLI's current MCP command and explicit OAuth action for separate setup.

## Requirements

- GitHub Copilot CLI installed and signed in.
- Browser access for OAuth.

## Install MCP Server

### Add the MCP server

```bash
copilot mcp add entalpa --type http --url https://api.entalpa.com/mcp
```

### Authenticate the MCP server

Start Copilot CLI and run `/mcp auth entalpa`, then complete the Entalpa browser authorization flow.

### Alternative interactive path

In Copilot CLI chat, use `/mcp add` and choose the HTTP transport.

## Install Entalpa Skill

Install from `entalpa/entalpa-mcp`'s default branch for the latest skill, or use a release tag for a reproducible install.

### Preferred Copilot plugin path

```bash
copilot plugin marketplace add entalpa/entalpa-mcp
copilot plugin install entalpa@entalpa-plugins
```

### GitHub CLI skill alternative

```bash
gh skill install entalpa/entalpa-mcp entalpa-implement --agent github-copilot --scope user
gh skill install entalpa/entalpa-mcp entalpa-prd --agent github-copilot --scope user
```

### npx skills alternative

```bash
npx skills add entalpa/entalpa-mcp --skill "*" --agent github-copilot -g -y
```

## Verify

- Use `/mcp show` in interactive mode, or `copilot mcp list` from the terminal, then ask Copilot CLI to list Entalpa projects.

## Known Limitations

- `/mcp search` registry discovery is experimental; document direct install as the reliable path.

## Sources

- [GitHub Copilot CLI command reference](https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-command-reference)
- [GitHub Copilot CLI MCP servers](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers)
- [GitHub Copilot CLI plugin reference](https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-plugin-reference)
- [GitHub CLI skills](https://cli.github.com/manual/gh_skill)
- [npx skills](https://github.com/vercel-labs/skills)
