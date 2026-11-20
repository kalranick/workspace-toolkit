---
name: create-pull-request
description: Create a well-described GitHub pull request from the current branch after reviewing changes and running focused validation.
---

# Create Pull Request

You create GitHub pull requests. Before creating a PR, inspect the repository state and make sure the proposal is safe and accurate.

## Workflow

1. Determine the target repository and branch:
   - Read `git status --short --branch` and `git remote -v`.
   - Identify the current branch and the repository's default branch.
   - Never create a PR from a detached HEAD or from the default branch unless the user explicitly approves it.
   - If there are unrelated uncommitted changes, stop and ask the user how to proceed.

2. Inspect the implementation:
   - Review `git diff --stat`, `git diff --cached`, and `git diff`.
   - Review recent commits that will be included with `git log`.
   - Compare the feature branch with the default branch, such as:
     `git diff <default-branch>...HEAD`
   - Do not summarize files without understanding the actual changes.

3. Validate the change:
   - Use the smallest relevant package scripts for the type of change.
   - Report failures instead of silently bypassing or masking them.
   - Do not modify source code unless needed to fix an issue discovered during the PR workflow.

4. Confirm PR details:
   - Choose the base branch. Use the repository default branch unless the user names another base.
   - Ensure commits are pushed to a remote branch.
   - Prefer `gh pr create --fill` only when the existing commits clearly provide an accurate title and body.
   - Otherwise, construct a concise title and a useful Markdown body.
   - Ask for confirmation before creating the PR if the title, body, base branch, draft state, or reviewers are uncertain.

5. Create the PR:
   - Use GitHub CLI via `gh`.
   - Use `--draft` when the user requests a draft or the change is not ready for review.
   - Push the branch before creation when it has no upstream branch or its commits are not pushed.
   - Link related issues using closing keywords only when the issue relationship is confirmed.
   - After creation, return the PR number and URL.

## PR Description Format

Use this structure unless repository conventions require otherwise:

```markdown
## Summary

- <1-3 concise bullets explaining what changed and why>

## Testing

- <command run and outcome>

## Notes

- <optional deployment, migration, configuration, or follow-up information>
```

## Safety Rules

- Never force-push.
- Never amend, rewrite, or delete commits.
- Never commit secrets, credentials, environment files, or generated data.
- Never merge or close a PR.
- Never add or remove labels, milestones, reviewers, assignees, or projects unless requested.
- Do not use broad destructive Git commands.
- Do not create a PR with uncommitted changes unless the user explicitly asks and the changes are intentional.
- Do not claim tests passed unless they were actually run successfully.
