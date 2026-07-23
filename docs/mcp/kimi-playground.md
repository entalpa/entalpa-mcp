# Kimi Playground

<!-- Generated from Entalpa's canonical integration source. -->

Add Entalpa directly as a remote MCP server in Kimi Playground, with ModelScope synchronization as an alternative hosted-service path.

## Requirements

- Kimi Playground access.
- Browser access if Kimi can complete Entalpa's OAuth flow in the selected authentication mode.
- ModelScope account and API token only when using the synchronization alternative.

## Install MCP Server

### Open Kimi Playground MCP settings

Log in to Kimi Playground, open MCP Server Settings, choose to add an MCP server, and enter or select the server URL, transport, and authentication method.

### Add Entalpa directly

Set the server URL to `https://api.entalpa.com/mcp`, select the remote HTTP or Streamable HTTP transport available in the UI, choose the OAuth authentication option if offered, and add the server.

### ModelScope synchronization alternative

Paste your ModelScope API token and start synchronization. Kimi imports configured hosted MCP services from your ModelScope account.

### Enable Entalpa in the conversation

After synchronization, select the Entalpa MCP service from the MCP Services List before using the conversation.

## Install Entalpa Skill

Install from `entalpa/entalpa-mcp`'s default branch for the latest skill, or use a release tag for a reproducible install.

### Use prompt guidance unless Skills appear

Kimi Playground's current official guidance does not establish a portable custom Skill install path. Use Entalpa server instructions and task prompt guidance, and describe skill installation only after Kimi publishes and validates that capability.

## Verify

- Confirm Entalpa appears in the Kimi Playground MCP Services List after direct setup or ModelScope sync.
- Ask Kimi to list Entalpa projects and verify that it calls the Entalpa MCP service.

## Known Limitations

- Kimi documents direct remote MCP configuration, but Entalpa's OAuth flow remains runtime-unverified in Playground.
- ModelScope remains an optional hosted alternative and requires an Entalpa-compatible hosted entry.
- Do not claim native custom Skill installation support for Kimi Playground without newer official documentation and runtime validation.

## Sources

- [Use MCP servers in Kimi Playground](https://platform.kimi.ai/docs/guide/use-playground-to-debug-the-model)
- [Kimi Playground](https://platform.kimi.ai/playground)
- [Kimi Playground ModelScope MCP configuration](https://platform.kimi.ai/docs/guide/configure-the-modelscope-mcp-server)
- [ModelScope MCP Plaza](https://modelscope.cn/mcp)
