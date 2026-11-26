---
name: repository-defaults
description: Manage GitHub repositories from ChatGPT using the custom GitHub Repo connection and the built-in GitHub connector where appropriate.
---

# Repository defaults

These are opt-in personal preferences. Explicit user instructions take precedence.

- Use the custom **GitHub Repo** plugin for repository creation, forks, file edits, bulk commits, workflow YAML edits, and other repository operations it supports.
- For personal repository creation, explicitly pass `private: false` and `autoInit: false` when unspecified; omit `organization`. Respect explicit visibility and initialization choices independently. Never change an existing repository's visibility to apply these defaults.
- Use the actual live tool schema. Do not invent creation parameters for licenses; add a license separately only when authorized and its type is known.
- Use the built-in **GitHub** connector for Actions runs, job logs, steps, artifacts, failed-job reruns, detailed CI status, and other operations unavailable in the custom plugin. Prefer its dedicated tools for these tasks; do not ask the user to select it again if it is already available. If a required connection is unavailable, explain what to connect.
- Respect explicit connector restrictions. Do not use another connector or retry another write route to bypass an authorization denial.
- Read the target repository, branch, and relevant files before editing. Initialize a truly empty repository with an authorized first file before using branch-based bulk writes. Do not initialize a create-only empty repository.
- When a requested change is ready and merging is authorized, merge its PR after applicable checks pass; do not leave a PR unnecessarily open. Respect branch protection and review requirements.
- Verify the resulting commit, CI run, release and actual versioned assets when applicable. Distinguish a submitted change from a successful build or release.
- On an uncertain write, inspect current state before retrying. On a denied operation, stop that route, report the actual error, and resolve permissions first.
- Workflow edits require OAuth `repo` and `workflow` in Base scopes for this setup. Scripts are useful for reusable build logic, not a requirement to avoid YAML edits.
