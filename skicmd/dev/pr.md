# /pr

Creates a pull request on GitHub.

## Parameters

- **$1** (optional): Target/base branch. Default: current branch.
- **$2** (optional): PR title. If omitted, auto-generate from commits.

## Usage

```
/pr                          # PR from current branch, auto-generate title
/pr develop                  # PR to develop branch
/pr main "Add login feature" # PR to main with custom title
```

## Instructions

1. Parse $1 (base branch) and $2 (title) from the user's input. Default base branch to the current branch (`git branch --show-current`).

2. Get the current branch name with `git branch --show-current`. If on the base branch, warn the user and stop.

3. Check if the branch is pushed to remote. If not, push it with `git push -u origin {current_branch}`.

4. Gather PR context:
   - Run `git log --oneline {$1}..HEAD` to list all commits in the branch.
   - Run `git diff {$1}...HEAD` to see the full diff against the base branch.

5. If $2 is provided, use it as the PR title. Otherwise, auto-generate a concise title (under 70 characters) from the commit history.

6. Generate the PR body:
   - `## Summary` — 1–3 bullet points describing the changes
   - `## Test plan` — checklist of testing steps based on the changes

7. Show the user the PR title and body for review. Ask to confirm, edit, or cancel.

8. Create the PR using:
   ```
   gh pr create --title "{title}" --body "{body}" --base {$1}
   ```

9. Report the PR URL to the user.
