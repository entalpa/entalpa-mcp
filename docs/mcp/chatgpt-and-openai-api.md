# ChatGPT and OpenAI API

<!-- Generated from Entalpa's canonical integration source. -->

Connect Entalpa to ChatGPT so you can ask it to pull in your project and turn it into a report, plan, or summary. This works on ChatGPT Pro, Business, Enterprise, and Edu, and through the OpenAI API for developers. On Pro, ChatGPT can read your Entalpa project but cannot save changes back to it.

## Requirements

- A ChatGPT account on Pro, Business, Enterprise, or Edu, or OpenAI API access if you are building your own tool. Pro can read your project; Business, Enterprise, and Edu can also let ChatGPT save changes back to Entalpa.
- On Business, Enterprise, or Edu, a workspace admin or owner may first need to turn on custom apps for you.
- A web browser to sign in to Entalpa when ChatGPT asks.

## Install MCP Server

### Turn on developer mode

Developer mode is a one-time switch that lets ChatGPT talk to outside apps like Entalpa. On Pro, open Settings, then Apps, then Advanced settings, and turn it on. On Business, Enterprise, or Edu, an admin or owner turns it on (Enterprise and Edu admins may first grant you access under Permissions and roles).

### Connect Entalpa

Add a new app named `Entalpa` with the address `https://api.entalpa.com/mcp`. Sign in with your Entalpa account when ChatGPT prompts you, and approve the tools it shows. On Business, Enterprise, and Edu, an admin then publishes the app to your workspace. On Pro you can connect the same address, but ChatGPT will only be able to read your project, not save changes.

### Ask ChatGPT to use your project

Start a new chat and ask ChatGPT to use Entalpa. For example, "Use Entalpa to open my Website Redesign project and write a one-page status report," or "Use Entalpa to open my project and draft an implementation plan." ChatGPT fetches your stories, requirements, and stakeholders and writes the document for you.

### Using the OpenAI API instead

For developers building their own tool with the OpenAI API rather than the ChatGPT app, complete Entalpa sign-in, then pass the access token in the Responses API MCP tool `authorization` field for calls to `https://api.entalpa.com/mcp`.

## Install Entalpa Skill

Install from `entalpa/entalpa-mcp`'s default branch for the latest skill, or use a release tag for a reproducible install.

### Optional, add the Entalpa skills

You only need these for the guided implementation and PRD/BRD workflows; they are not required for fetching a project or writing reports. In the ChatGPT sidebar, open Plugins, select the Skills tab, choose Create, then Upload from your computer, and upload the packaged `entalpa-implement` and `entalpa-prd` skills one at a time. ChatGPT, Codex, and API skills are stored separately.

### Optional, add the skills for API use

For OpenAI API workflows, create a hosted API skill from each `entalpa-implement` and `entalpa-prd` package and reference the required versions from the API tool or container that runs them. ChatGPT skills do not automatically sync to the API.

## Verify

- Ask ChatGPT "Use Entalpa to list my projects." It should sign you in if needed and then show your projects.

## Known Limitations

- On ChatGPT Pro, the Entalpa connection is read-only, so ChatGPT can pull in your project but cannot save changes back. Saving changes to Entalpa needs Business, Enterprise, or Edu, where full write access is currently in beta on the web.
- Apps and Skills are managed in different places (Apps versus the Plugins directory), so adding one does not add the other.
- ChatGPT agent mode does not use custom apps. Deep research can use them for reading only, not for saving changes.
- Skills do not currently sync across ChatGPT, Codex, and the API.

## Sources

- [ChatGPT developer mode](https://help.openai.com/en/articles/12584461-connectors-in-chatgpt)
- [Connect MCP servers from ChatGPT](https://developers.openai.com/apps-sdk/deploy/connect-chatgpt)
- [OpenAI tools and MCP connectors](https://developers.openai.com/api/docs/guides/tools-connectors-mcp)
- [OpenAI API MCP](https://developers.openai.com/api/docs/mcp)
- [Skills in ChatGPT](https://help.openai.com/en/articles/20001066)
- [Skills in the OpenAI API](https://developers.openai.com/api/docs/guides/tools-skills)
