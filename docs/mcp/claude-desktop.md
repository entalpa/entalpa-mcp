# Claude Desktop and Claude.ai

<!-- Generated from Entalpa's canonical integration source. -->

Use Claude custom connectors for the remote MCP server and Claude.ai's native custom-skill upload for the Entalpa workflow.

## Requirements

- Claude plan and client surface that supports custom connectors.
- Browser access for OAuth.
- Code execution enabled before using Skills in Claude.ai.

## Install MCP Server

### Open connector settings

In Free, Pro, or Max, open Customize, choose Connectors, then add a custom connector. Free accounts are limited to one custom connector. In Team or Enterprise plans, an Owner or Primary Owner adds custom connectors from Organization settings before members connect from Customize, Connectors.

### Enter the Entalpa connector details

Use name `Entalpa` and URL `https://api.entalpa.com/mcp`.

### Connect and authorize

Complete the Entalpa OAuth flow when Claude asks to connect.

## Install Entalpa Skill

Install from `entalpa/entalpa-mcp`'s default branch for the latest skill, or use a release tag for a reproducible install.

### Package the Entalpa skills

Create one ZIP per canonical skill directory, with the corresponding `entalpa-implement` or `entalpa-prd` folder from `skills/` at the archive root.

### Upload the custom skills

Open Customize, Skills, select the plus button, choose Create skill, then Upload a skill. Upload and enable each ZIP separately. Team and Enterprise owners can provision the skills organization-wide from Organization settings, Skills.

## Verify

- Ask Claude to show available Entalpa tools or list projects after connecting.

## Known Limitations

- Team or organization connector controls may hide custom connector setup.
- Claude.ai uses native ZIP upload rather than a local `npx skills` installation.

## Sources

- [Claude Custom Connectors](https://support.claude.com/en/articles/11175166-get-started-with-custom-connectors-using-remote-mcp)
- [Guide to the Figma MCP server](https://help.figma.com/hc/en-us/articles/32132100833559-Guide-to-the-Figma-MCP-server)
- [Use skills in Claude](https://support.claude.com/en/articles/12512180-use-skills-in-claude)
