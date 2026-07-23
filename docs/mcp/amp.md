# Amp

<!-- Generated from Entalpa's canonical integration source. -->

Use Amp's MCP configuration or `--mcp-config` for command-line runs, then install the Entalpa skills with `npx skills`.

## Requirements

- Amp installed and authenticated.
- Browser access for OAuth when the MCP server is first used.

## Install MCP Server

### One-shot CLI config

```bash
amp --mcp-config '{"entalpa":{"url":"https://api.entalpa.com/mcp"}}' -x "List Entalpa projects"
```

### Persistent MCP config

```bash
amp mcp add entalpa https://api.entalpa.com/mcp
```

## Install Entalpa Skill

Install from `entalpa/entalpa-mcp`'s default branch for the latest skill, or use a release tag for a reproducible install.

### Install the Entalpa skills

```bash
npx skills add entalpa/entalpa-mcp --skill "*" --agent amp -g -y
```

## Verify

- Run `amp mcp doctor` to check MCP approval/status workflows.
- Run Amp and ask it to list Entalpa projects.

## Known Limitations

- Exact persistent config location can vary by Amp surface; use `--mcp-config` for deterministic one-off verification.

## Sources

- [Amp manual](https://ampcode.com/manual)
- [npx skills](https://github.com/vercel-labs/skills)
