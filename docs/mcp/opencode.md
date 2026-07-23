# OpenCode

<!-- Generated from Entalpa's canonical integration source. -->

Use `opencode mcp add` or `opencode.json` with a remote MCP entry, then install the Entalpa skills.

## Requirements

- OpenCode installed.
- Browser access for OAuth if prompted.

## Install MCP Server

### Add interactively

```bash
opencode mcp add
```

### Manual config

```json
{
  "$schema": "https://opencode.ai/config.json",
  "mcp": {
    "entalpa": {
      "type": "remote",
      "url": "https://api.entalpa.com/mcp",
      "enabled": true
    }
  }
}
```

## Install Entalpa Skill

Install from `entalpa/entalpa-mcp`'s default branch for the latest skill, or use a release tag for a reproducible install.

### Install the Entalpa skills

```bash
npx skills add entalpa/entalpa-mcp --skill "*" --agent opencode -g -y
```

### GitHub CLI alternative

```bash
gh skill install entalpa/entalpa-mcp entalpa-implement --agent opencode --scope user
gh skill install entalpa/entalpa-mcp entalpa-prd --agent opencode --scope user
```

## Verify

- Run `opencode mcp list` and confirm Entalpa appears in configured MCP servers.
- If authentication is pending, run `opencode mcp auth entalpa`.
- Ask OpenCode to list Entalpa projects.

## Known Limitations

- Prefer the guided command when possible because OpenCode config schema can evolve.

## Sources

- [OpenCode CLI](https://opencode.ai/docs/cli/)
- [OpenCode MCP servers](https://opencode.ai/docs/mcp-servers/)
- [npx skills](https://github.com/vercel-labs/skills)
- [GitHub CLI skills](https://cli.github.com/manual/gh_skill)
