# /review

Reviews staged and unstaged code changes before committing.

## Parameters

- **$1** (optional): Specific file path to review. If omitted, review all changed files.

## Usage

```
/review                      # review all uncommitted changes
/review src/main.py          # review changes in a specific file
```

## Instructions

1. Parse $1 from the user's input.

2. **Gather changes**:
   - Run `git status` to list modified, staged, and untracked files.
   - If $1 is provided, scope to that file only.
   - Run `git diff` (unstaged) and `git diff --cached` (staged) to get the actual changes.
   - If there are no changes, inform the user and stop.

3. **Review each changed file** for:
   - **Bugs**: Logic errors, off-by-one, null/undefined access, incorrect conditions
   - **Security**: Hardcoded secrets, injection risks, unsafe input handling
   - **Leftover debug code**: `print()`, `console.log()`, `debugger`, `TODO`/`FIXME` comments
   - **Style**: Inconsistent naming, unused imports or variables, formatting issues
   - **Completeness**: Missing error handling, incomplete implementations, placeholder code

4. **Present findings** grouped by file, with line numbers and severity:
   - **Block**: Must fix before committing
   - **Warn**: Should consider fixing
   - **Info**: Minor suggestions

5. If no issues found, confirm the changes look good and are ready to commit.

6. If issues are found, ask the user which fixes to apply. Apply approved fixes.

7. After fixes, re-run `git diff` to show the updated changes for final confirmation.
