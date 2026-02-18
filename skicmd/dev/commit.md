# /commit

Stages, reviews, and commits changes in one workflow.

## Parameters

- **$1** (optional): Commit message. If omitted, auto-generate from the changes.

## Usage

```
/commit                              # auto-generate commit message
/commit "Fix login validation bug"   # use provided message
```

## Instructions

1. Run `git status` to see all modified, staged, and untracked files. If there are no changes, inform the user and stop.

2. Run `git diff` and `git diff --cached` to see the full set of changes.

3. Present a summary of all changes grouped by status (modified, new, deleted) and ask the user which files to stage. Options: all, specific files, or already-staged only.

4. Stage the selected files with `git add`.

5. **Review** the staged changes for:
   - Leftover debug code (`print()`, `console.log()`, `debugger`)
   - Hardcoded secrets or credentials
   - TODO/FIXME comments that shouldn't be committed
   - Unintended files (`.env`, large binaries, IDE configs)
   If issues are found, warn the user and ask whether to fix, unstage, or proceed anyway.

6. If $1 is provided, use it as the commit message. If omitted, analyze the staged diff and generate a concise commit message:
   - Summarize the nature of the changes (add, update, fix, refactor, etc.)
   - Focus on the "why" rather than the "what"
   - Keep to 1–2 sentences

7. Show the proposed commit message and ask the user to confirm, edit, or cancel.

8. Create the commit with the approved message.

9. Run `git status` to confirm the commit succeeded and report the result.
