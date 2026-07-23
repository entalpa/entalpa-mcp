# Replit

<!-- Generated from Entalpa's canonical integration source. -->

Replit supports custom MCP servers, install links, and Agent Skills when the workspace plan exposes those features. Use Core as the conservative starting assumption and verify the actual plan before setup.

## Requirements

- Replit workspace whose plan exposes Agent MCP servers and Skills; assume Core or higher unless the current workspace UI proves otherwise.
- Browser access for OAuth.

## Install MCP Server

### Add a custom MCP server

In Replit MCP Servers settings, choose Add MCP server, set display name `Entalpa`, and enter `https://api.entalpa.com/mcp`.

### Candidate install link

Replit install links encode a JSON payload with `displayName` and `baseUrl`. Generate one only after validating Entalpa OAuth in Replit.

## Install Entalpa Skill

Install from `entalpa/entalpa-mcp`'s default branch for the latest skill, or use a release tag for a reproducible install.

### Install the Entalpa project skills

```bash
npx skills add entalpa/entalpa-mcp --skill "*" --agent replit -y
```

### Replit Skills pane alternative

In the current Replit project, open the Skills pane and install or attach `entalpa-implement` and `entalpa-prd` from this repository, then enable both for the Agent session.

## Verify

- Confirm Replit Agent can see Entalpa tools and list projects.

## Known Limitations

- Do not publish a one-click Replit install link until the OAuth flow has been tested end to end.
- Replit feature access is plan-dependent and can change. Core is a working assumption because it includes Agent and connectors, not a guarantee that every Core workspace exposes custom MCP and Skills.

## Sources

- [Replit Connect via MCP](https://docs.replit.com/build/connect-via-mcp)
- [Replit Starter plan connector limits](https://docs.replit.com/billing/plans/starter-plan)
- [Replit MCP install links](https://docs.replit.com/references/mcp/install-links)
- [Replit Agent Skills](https://docs.replit.com/build/use-agent-skills)
- [npx skills](https://github.com/vercel-labs/skills)
