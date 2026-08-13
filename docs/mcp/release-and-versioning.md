# Entalpa MCP Release and Versioning

<!-- Generated from Entalpa's canonical integration source. -->

Use release tags when you need reproducible skill or plugin installs. The unpinned `npx skills` and plugin commands below track the repository default branch. GitHub CLI skill installs resolve the latest tagged release first, then default branch HEAD.

## Current Version

- Distribution version: `0.1.2`
- Plugin version: `0.1.2`
- Recommended release tag: `v0.1.2`

The distribution, registry metadata, and plugin manifests derive these values from one canonical release version.

The pinned commands below intentionally use `<release-tag>` as a placeholder. Replace it with `v0.1.2` only after that tag exists in `entalpa/entalpa-mcp`.



## Pinned Codex Plugin Marketplace

Codex marketplace sources support repository refs. Use this after the release tag exists:

```bash
codex plugin marketplace add entalpa/entalpa-mcp@<release-tag> --sparse .agents/plugins --sparse plugins
codex plugin add entalpa@entalpa-plugins
```

The marketplace command pins the catalog source; the plugin command installs `entalpa`. You can use `/plugins` instead of the second command.

## Pinned Claude Code Plugin Marketplace

Claude Code plugin marketplace sources also support repository refs. Use this after the release tag exists:

```bash
claude plugin marketplace add entalpa/entalpa-mcp@<release-tag> --sparse .claude-plugin plugins
claude plugin install entalpa@entalpa-plugins
```

## Pinned Skill Install

`npx skills` supports repository refs and explicit all-skill selection. Use this after the release tag exists:

```bash
npx skills add https://github.com/entalpa/entalpa-mcp/tree/<release-tag> --skill "*" --agent codex -g -y
```

This installs all configured skills (`entalpa-implement`, `entalpa-prd`). Change `--agent codex` to another supported agent when needed.

GitHub CLI also supports pinned skill installs:

```bash
gh skill install entalpa/entalpa-mcp entalpa-implement --pin <release-tag> --agent codex --scope user
gh skill install entalpa/entalpa-mcp entalpa-prd --pin <release-tag> --agent codex --scope user
```

To use either skill without installing it:

```bash
npx skills use https://github.com/entalpa/entalpa-mcp/tree/<release-tag>/skills/entalpa-implement
npx skills use https://github.com/entalpa/entalpa-mcp/tree/<release-tag>/skills/entalpa-prd
```

## Unpinned Current Installs

Use these when you intentionally want the latest default-branch docs and skills:

These commands install the latest skill and plugin artifacts from `entalpa/entalpa-mcp`'s default branch.

```bash
npx skills add entalpa/entalpa-mcp --skill "*" --agent codex -g -y
codex plugin marketplace add entalpa/entalpa-mcp --sparse .agents/plugins --sparse plugins
codex plugin add entalpa@entalpa-plugins
```

## Sources

- [Codex Plugins](https://learn.chatgpt.com/docs/plugins)
- [Build Codex plugins](https://developers.openai.com/plugins/build/plugins)
- [Codex 0.147.0 plugin MCP parser](https://github.com/openai/codex/blob/rust-v0.147.0/codex-rs/codex-mcp/src/plugin_config.rs#L35-L50)
- [Submit plugins to the OpenAI plugin directory](https://developers.openai.com/plugins/deploy/submission)
- [Claude Code plugin marketplaces](https://code.claude.com/docs/en/plugin-marketplaces)
- [npx skills](https://github.com/vercel-labs/skills)
- [GitHub CLI skills](https://cli.github.com/manual/gh_skill)
- [GitHub CLI skill publishing](https://cli.github.com/manual/gh_skill_publish)
