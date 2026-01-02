# Publish Command

This command commits all changes, pushes them to the remote branch, creates a pull request, and merges it to main to publish the content.

## Instructions

**IMPORTANT: Before executing ANY of the steps below, you MUST ask the user for confirmation.**

Display this message to the user:

---
**PUBLISH CONFIRMATION REQUIRED**

You are about to publish your changes. This will:
1. Commit all current changes
2. Push to the remote branch
3. Create a Pull Request to main
4. Merge the PR to publish the content

**Are you sure you want to proceed?** (yes/no)

---

**Wait for the user's explicit confirmation before proceeding.**

## Execution Steps (Only after confirmation)

If the user confirms with "yes", "y", "si", "sí", or similar affirmative response:

1. **Check for changes**: Run `git status` to see what changes exist
2. **Stage all changes**: Run `git add -A`
3. **Commit changes**: Create a commit with message "Publish: Update content [timestamp]"
4. **Push to remote**: Push the current branch to origin with `git push -u origin [branch-name]`
5. **Create Pull Request**: Use `gh pr create --title "Publish content update" --body "Automated publish of content updates"`
6. **Merge PR**: Use `gh pr merge --merge --auto` to merge the PR to main

## Error Handling

- If there are no changes to commit, inform the user and stop
- If push fails, retry up to 4 times with exponential backoff
- If PR creation fails, check if a PR already exists and use that one
- If merge fails, inform the user and provide the PR URL for manual review

## Success Message

After successful execution, display:

---
**PUBLISHED SUCCESSFULLY**

Your changes have been published to main.
- Commit: [commit hash]
- PR: [PR URL]
- Status: Merged

---
