# /allow

Adds a tool/app permission to `.claude/settings.local.json` in the current project.

## Parameters

- **$1** (required): Tool name (e.g. `git`) or path/wildcard pattern (e.g. `~/.claude/commands/*`)
- **$2** (optional): Specific tool type to scope the permission to (e.g. `Bash`, `Read`, `Edit`). If omitted, allows across all tool types.

## Usage

```
/allow git                          # adds Bash(git:*), PowerShell(git:*), Read(git:*), Edit(git:*), Write(git:*)
/allow npm Bash                     # adds only Bash(npm:*)
/allow ~/.claude/commands/* Bash    # adds Bash(~/.claude/commands/*)
/allow ~/.claude/commands/*         # adds for all tool types with wildcard path
```

## Instructions

1. Parse $1 from the user's input. If missing, default to allowing: `git`, `pip`, `python`, `gh`. Show the list and ask the user to confirm before proceeding.

2. Parse $2 from the user's input. If missing, apply to all tool types: `Bash`, `PowerShell`, `Read`, `Edit`, `Write`.

3. Read `.claude/settings.local.json` in the current working directory. If it doesn't exist, create it with this structure:
   ```json
   {
     "permissions": {
       "allow": []
     }
   }
   ```

4. Determine if $1 is a **path/wildcard** (contains `/` or `*`) or a **simple tool name**:
   - **Path/wildcard**: use pattern as-is → `{$2}({$1})`
   - **Simple name**: append `:*` → `{$2}({$1}:*)`

5. Construct the permission entries:
   - If $2 is provided: single entry. Proceed to step 7.
   - If $2 is omitted: one entry per tool type (`Bash`, `PowerShell`, `Read`, `Edit`, `Write`).

6. If $2 was omitted (all tool types), show the list of entries that will be added and ask the user to confirm before proceeding.

7. Skip any entries that already exist in the `allow` array.

8. Add the new entries to the `permissions.allow` array and write the file.

9. **Post-install cleanup**: Review the full settings file for:
   - **Duplicates**: Remove any duplicate entries within the `allow` array.
   - **Conflicts**: If the same pattern exists in both `allow` and `deny`, warn the user and ask which to keep.
   - **Redundancies**: If a wildcard entry (e.g. `Bash(git:*)`) covers a more specific entry (e.g. `Bash(git commit:*)`), prompt to remove the specific one.

10. Confirm what was added and show the updated allow list.
