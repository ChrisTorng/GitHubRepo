# GitHubRepo

<img src="assets/repo-plus.png" width="80" alt="Repository with plus sign">

Connect ChatGPT to [GitHub's hosted MCP server](https://github.com/github/github-mcp-server) using your own OAuth app. Create and fork repositories, edit files, and modify GitHub Actions workflows directly in chat, without hosting a server or using a PAT.

This is an independent setup guide and optional Skill, not a new MCP server or an official GitHub/OpenAI product.

## Setup

1. In [ChatGPT Plugins](https://chatgpt.com/plugins), choose **+ → Add custom MCP server** (enable developer mode if required). Enter a name such as **GitHub Repo**, and server URL `https://api.githubcopilot.com/mcp/`. Select OAuth and note the displayed callback URL.
2. [Register your own GitHub OAuth app](https://github.com/settings/applications/new). Use a name such as **GH Repo for ChatGPT**, your homepage, and the exact callback URL from ChatGPT. Generate a client secret. Leave wildcard matching and Device Flow disabled.
3. In ChatGPT, open **Advanced OAuth settings**:

| Setting | Value |
|---|---|
| Registration | User-Defined OAuth Client |
| Client ID / secret | Your own OAuth app credentials |
| Token endpoint auth | `client_secret_post` |
| Authorization URL | `https://github.com/login/oauth/authorize` |
| Token URL | `https://github.com/login/oauth/access_token` |
| Default scopes | `repo` (additional scopes as needed) |
| Base scopes | `repo` and `workflow` (one per line) |
| Registration URL | Empty |
| Resource | `https://api.githubcopilot.com/mcp/` |

Keep valid automatically discovered settings. Use the callback shown in your own form (our test used `https://chatgpt.com/connector_platform_oauth_redirect`). Never publish secrets, authorization codes, or tokens.

4. Create the plugin, connect your account, and review the GitHub authorization. In a new chat select the plugin and ask it to call `get_me`. Then test a repository operation you actually intend to perform.

## Why Base scopes matter

An initial authorization with only `repo` worked for repository creation and ordinary commits but failed when editing `.github/workflows/`. GitHub's remote MCP supports on-demand scope challenges; in our ChatGPT setup, reauthorization did not add the required scope. Refreshing tools did not fix it.

Creating a new connection with **Base scopes** `repo` and `workflow` fixed the problem: a real workflow edit succeeded. GitHub's OAuth app settings do not have a scope checkbox; the OAuth client requests scopes. If the existing ChatGPT app does not expose Base scope editing, recreate the ChatGPT connection, not the GitHub OAuth app.

These scopes grant broad repository access. If you only need read-only access, use a narrower connection instead.

## Optional Skill

[repository-defaults/SKILL.md](skills/repository-defaults/SKILL.md) is an opt-in example for consistent repository management. Add it to your custom plugin using Plugin Creator, or adapt its rules for your own preferences. It does not grant OAuth permissions.

| Use the custom GitHub Repo plugin | Use ChatGPT's built-in GitHub connector |
|---|---|
| Create/fork repositories, bulk file edits, workflow YAML, PRs/issues | Actions jobs/logs/artifacts, reruns, CI verification and missing tools |

Tool availability varies by account and platform. Explicit connector preferences and approval requirements take precedence.

## Verification

Tested in ordinary ChatGPT chat: account lookup, repository creation, multi-file commits, workflow edits and GitHub Actions release verification using the built-in connector. No standalone MCP server or shared credential is required. See [examples](examples/prompts.md), [tools](docs/tools.md) and [troubleshooting](docs/attempts.md).

## References

- [GitHub MCP Server](https://github.com/github/github-mcp-server)
- [OAuth scope challenges](https://github.com/github/github-mcp-server/blob/main/docs/scope-filtering.md#oauth-scope-challenges-remote-server)
- [GitHub OAuth scopes](https://docs.github.com/en/apps/oauth-apps/building-oauth-apps/scopes-for-oauth-apps)
- [Custom MCP servers in ChatGPT](https://help.openai.com/en/articles/12584461-connecting-custom-mcp-servers-in-chatgpt)

[MIT License](LICENSE) covers this project's original documentation, Skill and icon, not third-party services or trademarks.
