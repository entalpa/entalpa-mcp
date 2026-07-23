# Entalpa MCP Troubleshooting

<!-- Generated from Entalpa's canonical integration source. -->

## OAuth Does Not Open

- Confirm the client supports remote Streamable HTTP MCP servers with OAuth.
- Re-run the client's native MCP login command when available.
- Check whether the client requires a fixed callback port or pre-registered redirect URI.
- Try the same server in Codex or Claude Code to separate Entalpa server issues from client-specific issues.

## Server Is Added But Tools Are Missing

- Restart the client or reload MCP servers from the client's MCP settings.
- Confirm the server URL is exactly `https://api.entalpa.com/mcp`.
- Confirm the transport is Streamable HTTP. Some clients use `http`, `streamable-http`, or `httpUrl` to mean this.
- Ask for a simple read-only call first, such as `users_get_me` or `projects_list`.

## Authentication Succeeds But Project Data Is Empty

- Confirm the Entalpa account belongs to the expected workspace or project.
- Use `users_get_me` to verify the authenticated identity.
- Use `projects_list` before targeting a project by ID.

## Skills Are Installed But Not Used

- Invoke the relevant skill explicitly as `$entalpa-implement` or `$entalpa-prd`.
- Confirm the target agent is supported by the skill installer.
- Use GitHub CLI as an alternative when it supports the target agent; install each skill explicitly:

```bash
gh skill install entalpa/entalpa-mcp entalpa-implement --agent <agent> --scope user
gh skill install entalpa/entalpa-mcp entalpa-prd --agent <agent> --scope user
```

## GitHub Copilot Cloud Agent

Do not use the GitHub repository/cloud-agent MCP configuration for Entalpa yet. GitHub's current documentation limits remote MCP OAuth support for that surface. VS Code and Copilot CLI remain separate local-client paths.

## Sources

- [Codex MCP](https://developers.openai.com/codex/mcp)
- [Claude Code MCP](https://code.claude.com/docs/en/mcp)
- [Configure MCP servers for GitHub Copilot coding agent](https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/configure-mcp-servers)
- [npx skills](https://github.com/vercel-labs/skills)
