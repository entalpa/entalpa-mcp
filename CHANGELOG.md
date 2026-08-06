# Changelog

Notable changes to the Entalpa MCP integrations: the remote MCP connection, the
published Agent Skills, and the Codex and Claude Code plugin bundle.

Versions follow the canonical distribution release, so `0.1.0` here is the same
`0.1.0` a client reports for the installed plugin. This changelog and the
canonical skills are maintained by hand; generated documentation, marketplace
metadata, and plugin skill copies are derived from the source configuration.

## Unreleased

- Documentation: the Codex documentation links now point at their current
  locations. Every `developers.openai.com/codex/*` URL had started answering
  `308` and redirecting elsewhere.
- Documentation: pinned install examples in the canonical public artifact name
  `v0.1.0`, which exists in `entalpa/entalpa-mcp`; internal and repository-
  override builds retain a `<release-tag>` placeholder.
- Documentation: the README states that an Entalpa account is required, and
  links the MCP support page, support address, privacy policy, and terms of
  service.

## 0.1.0 - 2026-07-23

First public release.

- Remote MCP server at `https://api.entalpa.com/mcp` over Streamable HTTP,
  authenticated with OAuth. Clients register themselves; there is no API key.
- Agent Skills `entalpa-implement` (implement requirements and record code
  references, status, and test coverage back onto them) and `entalpa-prd`
  (generate a PRD or BRD document from a project).
- Plugin bundle installable from the repository marketplace in Codex and Claude
  Code, which adds the MCP connection and both skills together.
- Client-by-client installation and troubleshooting guides for the supported
  MCP clients under `docs/mcp/`.
