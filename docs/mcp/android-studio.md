# Android Studio Gemini

<!-- Generated from Entalpa's canonical integration source. -->

Android Studio can load MCP server JSON for Gemini Agent Mode. Add Entalpa as a remote HTTP MCP server when the installed version supports remote MCP.

## Requirements

- Android Studio with Gemini Agent Mode and MCP server support.
- Browser access for OAuth.

## Install MCP Server

### Add through Android Studio settings

Open File or Android Studio Settings, then Tools, AI, MCP Servers. Enable MCP Servers and add the Entalpa configuration.

### MCP config

```json
{
  "mcpServers": {
    "entalpa": {
      "httpUrl": "https://api.entalpa.com/mcp"
    }
  }
}
```

## Install Entalpa Skill

Install from `entalpa/entalpa-mcp`'s default branch for the latest skill, or use a release tag for a reproducible install.

### Native skill support

Android Studio Gemini Agent Mode supports Agent Skills from `.agents/skills` or `.android-studio/skills` under the project root or home directory. `npx skills` does not currently list an Android Studio target, so use native skill placement after validating the installed version.

## Verify

- In Agent Mode, ask Gemini to list Entalpa projects or available tools.

## Known Limitations

- Android Studio MCP support is version-sensitive. Validate OAuth behavior before treating it as a primary path.

## Sources

- [Android Studio MCP servers](https://developer.android.com/studio/gemini/add-mcp-server)
- [Android Studio Gemini skills](https://developer.android.com/studio/gemini/skills)
- [npx skills](https://github.com/vercel-labs/skills)
