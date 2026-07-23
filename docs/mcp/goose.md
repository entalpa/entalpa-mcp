# Goose

<!-- Generated from Entalpa's canonical integration source. -->

Add Entalpa as a remote Goose extension backed by MCP, then install the Entalpa skills where the current Goose version supports local skills.

## Requirements

- Goose installed.
- Browser access for OAuth.

## Install MCP Server

### Open extension setup

```bash
goose configure
```

### Add remote extension

Choose Add Extension, then Remote Extension (Streamable HTTP), name it `entalpa`, and use URL `https://api.entalpa.com/mcp`.

## Install Entalpa Skill

Install from `entalpa/entalpa-mcp`'s default branch for the latest skill, or use a release tag for a reproducible install.

### Goose compatibility skill installer

```bash
npx skills add entalpa/entalpa-mcp --skill "*" --agent goose -g -y
```

### GitHub CLI alternative

```bash
gh skill install entalpa/entalpa-mcp entalpa-implement --agent goose --scope user
gh skill install entalpa/entalpa-mcp entalpa-prd --agent goose --scope user
```

## Verify

- Start Goose and ask it to list Entalpa projects.

## Known Limitations

- Goose official skills docs emphasize `.agents/skills` paths. `npx skills --agent goose` currently targets Goose-compatible locations, so validate placement against the installed Goose version.

## Sources

- [Goose extensions](https://goose-docs.ai/docs/getting-started/using-extensions/)
- [FastMCP Goose integration](https://gofastmcp.com/integrations/goose)
- [npx skills](https://github.com/vercel-labs/skills)
- [GitHub CLI skills](https://cli.github.com/manual/gh_skill)
