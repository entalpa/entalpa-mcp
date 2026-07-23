# Docker MCP Catalog and Toolkit

<!-- Generated from Entalpa's canonical integration source. -->

Prepare Entalpa as a remote-service candidate for Docker's MCP Catalog, whose Toolkit can handle browser OAuth after the catalog entry is accepted.

## Requirements

- Docker Desktop with MCP Toolkit when testing catalog or gateway workflows.
- An accepted Entalpa remote-service entry in Docker's `mcp-registry` before advertising end-user installation.

## Install MCP Server

### Prepare the remote-service entry

Fork `docker/mcp-registry`, run `task remote-wizard`, and define Entalpa's Streamable HTTP URL `https://api.entalpa.com/mcp`, product metadata, dynamic tool discovery metadata, public documentation, and OAuth authentication requirements.

### Submit and wait for acceptance

Open the registry pull request and complete Docker's validation and review. Do not publish Docker install instructions until the entry appears in Docker Desktop MCP Toolkit and the Docker MCP Catalog.

### Validate Toolkit OAuth after acceptance

Run `docker mcp oauth authorize entalpa`, complete the browser flow, then open Docker Desktop MCP Toolkit, find Entalpa in the Catalog, and add it to a profile.

### Connect a downstream agent

Attach the validated profile through Docker MCP Gateway to a supported coding agent, then confirm the agent can list Entalpa projects.

## Install Entalpa Skill

Install from `entalpa/entalpa-mcp`'s default branch for the latest skill, or use a release tag for a reproducible install.

### Skill status

Docker MCP Toolkit is not a coding-agent skill host. Install `entalpa-implement` and `entalpa-prd` in the downstream agent that consumes Docker-managed MCP servers.

## Verify

- Validate any future catalog entry in Docker Desktop MCP Toolkit before advertising it.

## Known Limitations

- Docker MCP Catalog includes packaged servers and hosted remote services, but do not imply Entalpa is listed until a submission is accepted.
- Docker's general remote OAuth support is documented, but Entalpa's catalog entry and end-to-end OAuth flow remain candidates until accepted and tested.

## Sources

- [Contribute remote servers to the Docker MCP Registry](https://github.com/docker/mcp-registry/blob/main/CONTRIBUTING.md)
- [Docker MCP Catalog](https://docs.docker.com/ai/mcp-catalog-and-toolkit/catalog/)
- [Docker MCP Catalog and Toolkit](https://docs.docker.com/ai/mcp-catalog-and-toolkit/)
