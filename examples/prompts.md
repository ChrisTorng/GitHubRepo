# Example prompts

Select your own custom GitHub Repo plugin in ChatGPT.

- **Read-only check:** "Use GitHub Repo's get_me to verify my account. Do not write anything."
- **Create a repository:** "Create a public, empty personal repository named MY_ACTUAL_REPO using GitHub Repo. Do not initialize it or add files." Replace the name before sending.
- **Workflow edit:** "Update the existing workflow in OWNER/REPO, commit the authorized change, and verify the CI run. Use the built-in GitHub connector for logs and artifacts if needed."
- **Uncertain write:** "Check the current branch and commit before retrying. Report the actual authorization error."

For persistent preferences, see the [optional Skill](../skills/repository-defaults/SKILL.md). It does not change API defaults, permissions, or the available tool list.
