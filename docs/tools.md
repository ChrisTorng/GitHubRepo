# Tool coverage

The custom GitHub Repo connection exposed 45 tools in our November 2026 session, including:

| Category | Examples |
|---|---|
| Repositories | create_repository, fork_repository, search_repositories |
| Files and Git | get_file_contents, create_or_update_file, push_files, create_branch, get_commit |
| Pull requests | create_pull_request, merge_pull_request, pull_request_read, pull_request_review_write |
| Issues | issue_read, issue_write, list_issues, add_issue_comment |
| Releases and tags | list_releases, get_latest_release, get_release_by_tag, list_tags |
| Account and teams | get_me, get_teams, search_users |

The built-in GitHub connector complements it with dedicated Actions run/job/log/artifact tools, CI status and additional PR operations. The exposed tools depend on the connection and session; inspect live schemas instead of relying on a fixed list.

For personal repository creation, explicitly specify `private` and `autoInit`. The tested creation tool does not accept a license parameter. Do not assume that a visible tool has every required OAuth scope.
