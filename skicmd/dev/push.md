# /push

Pushes commits to a remote repository.

## Parameters

- **$1** (optional): Remote name. Default: `origin`.
- **$2** (optional): Branch name. Default: current branch.

## Usage

```
/push                        # push current branch to origin
/push origin main            # push to origin/main
/push upstream dev            # push to upstream/dev
```

## Instructions

1. Parse $1 (remote) and $2 (branch) from the user's input. If missing, default to `origin` and the current branch (`git branch --show-current`).

2. Run `git status` to check:
   - If there are uncommitted changes, warn the user and ask whether to proceed or commit first.
   - If the branch has no unpushed commits (`git log {remote}/{branch}..HEAD`), inform the user there's nothing to push and stop.

3. Show the user what will be pushed:
   - Remote and branch target
   - Number of commits ahead
   - Brief log of commits to be pushed (`git log --oneline {remote}/{branch}..HEAD`)

4. Ask the user to confirm before pushing.

5. Run `git push {$1} {$2}`. If pushing a new branch that has no upstream, use `git push -u {$1} {$2}`.

6. If the push fails (e.g. rejected, auth error, no remote), report the error and suggest a fix.

7. Confirm success and show the remote URL.
