# Claude Desktop and Claude.ai

<!-- Generated from Entalpa's canonical integration source. -->

Add the Entalpa plugin from Claude's plugin directory to get the remote MCP server and every Entalpa skill in chat, Cowork and Claude Code. Where the directory is not available, add Entalpa as a custom connector and upload the skills yourself.

## Requirements

- For the directory plugin: a Pro, Max, Ultra, Team or Enterprise plan. On a Free plan, use the custom connector.
- Browser access for OAuth.
- Code execution enabled before using Skills in Claude.ai.

## Install MCP Server

### Add the Entalpa plugin from the directory

In claude.ai or the Claude desktop app, open [Customize, Plugins](https://claude.ai/customize/plugins), search for Entalpa on the Discover tab, and select Add. The plugin is saved to your Claude account, so it also loads in Cowork and in Claude Code without a second install.

### Connect the Entalpa connector

Open the plugin, select its Connectors tab, then add and connect `entalpa` and complete the Entalpa OAuth flow. On Team and Enterprise plans, an Owner decides whether the directory's plugins are available and adds the connector for the organization from Organization settings, Connectors; members then connect it with their own account.

### Fallback: add a custom connector

If the directory is not available to you, open Customize, Connectors and add a custom connector with name `Entalpa` and URL `https://api.entalpa.com/mcp`, then complete the OAuth flow when Claude asks to connect. [This link](https://claude.ai/customize/connectors?modal=add-custom-connector&connectorName=Entalpa&connectorUrl=https%3A%2F%2Fapi.entalpa.com%2Fmcp) opens the dialog with both values filled in. Free accounts are limited to one custom connector. In Team or Enterprise plans, an Owner or Primary Owner adds custom connectors from Organization settings before members connect from Customize, Connectors.

## Install Entalpa Skill

Install from `entalpa/entalpa-mcp`'s default branch for the latest skill, or use a release tag for a reproducible install.

### Preferred plugin path

The directory plugin includes every Entalpa skill, so there is nothing more to install. With the custom connector fallback, upload the skills as described below.

### Package the Entalpa skills

Create one ZIP per canonical skill directory, with the corresponding `entalpa-implement`, `entalpa-prd`, `entalpa-openspec` or `entalpa-speckit` folder from `skills/` at the archive root.

### Upload the custom skills

Open Customize, Skills, select the plus button, choose Create skill, then Upload a skill. Upload and enable each ZIP separately. Team and Enterprise owners can provision the skills organization-wide from Organization settings, Skills.

## Verify

- Ask Claude to show available Entalpa tools or list projects after connecting.
- With the plugin, type `/` in the message box; the Entalpa skills are listed under the plugin's name.

## Known Limitations

- The directory's plugins appear on Pro, Max, Ultra, Team and Enterprise plans. On Team and Enterprise, an Owner can remove the directory as a source or keep its plugins unavailable to members.
- Adding the plugin does not connect anything. Its skills load at once, but they reach Entalpa only after the connector shows Connected.
- Team or organization connector controls may hide custom connector setup.
- Without the plugin, Claude.ai uses native ZIP upload rather than a local `npx skills` installation.

## Sources

- [Plugins in Claude](https://claude.com/docs/plugins/overview)
- [Plugin feature support across platforms](https://claude.com/docs/plugins/platform-support)
- [Manage plugins for your organization](https://claude.com/docs/plugins/admin)
- [Claude Custom Connectors](https://support.claude.com/en/articles/11175166-get-started-with-custom-connectors-using-remote-mcp)
- [Custom connector install link](https://claude.com/docs/connectors/building/directory-vs-custom#custom-connector-install-link)
- [Guide to the Figma MCP server](https://help.figma.com/hc/en-us/articles/32132100833559-Guide-to-the-Figma-MCP-server)
- [Use skills in Claude](https://support.claude.com/en/articles/12512180-use-skills-in-claude)
