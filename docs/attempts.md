# Troubleshooting

| Symptom | What to check |
|---|---|
| Couldn't register an OAuth client | Use your own registered OAuth app and `client_secret_post`. Do not invent a DCR registration URL. |
| Read/write works but workflow edits fail | Ensure Base scopes contain both `repo` and `workflow`. Recreate the ChatGPT connection if editing scopes is unavailable. |
| Failed to connect app | Check `get_me`, branch state, and exact tool error. A host authorization failure does not prove GitHub received the write. |
| Missing Actions logs or artifacts | Use ChatGPT's built-in GitHub connector if it provides the required tools. |
| Want only one tool | GitHub supports tool filtering headers, but our ChatGPT custom connection did not expose a custom header field. A Skill is not a tool allowlist. |

Do not confuse ChatGPT's action approval settings with GitHub OAuth scopes. Do not retry ambiguous writes before checking the branch or repository state.

The setup was verified with user-defined OAuth credentials. Built-in client registration and single-tool filtering were not verified in our custom ChatGPT connection. No custom proxy, shared PAT service, or public plugin listing is required.

- [Remote MCP server](https://github.com/github/github-mcp-server/blob/main/docs/remote-server.md)
- [Scope challenges](https://github.com/github/github-mcp-server/blob/main/docs/scope-filtering.md)
