# /deny

Adds a tool/app denial to `.claude/settings.local.json` in the current project.

## Parameters

- **$1** (required): Tool name (e.g. `rm`) or path/wildcard pattern (e.g. `~/.claude/commands/*`)
- **$2** (optional): Specific tool type to scope the denial to (e.g. `Bash`, `Read`, `Edit`). If omitted, denies across all tool types.

## Usage

```
/deny rm                            # adds Bash(rm:*), PowerShell(rm:*), Read(rm:*), Edit(rm:*), Write(rm:*)
/deny docker Bash                   # adds only Bash(docker:*)
/deny ~/.claude/commands/* Bash     # adds Bash(~/.claude/commands/*)
/deny ~/.claude/commands/*          # adds for all tool types with wildcard path
```

## Instructions

1. Parse $1 from the user's input. If missing, ask the user which tool to deny.

2. Parse $2 from the user's input. If missing, apply to all tool types: `Bash`, `PowerShell`, `Read`, `Edit`, `Write`.

3. Read `.claude/settings.local.json` in the current working directory. If it doesn't exist, create it with this structure:
   ```json
   {
     "permissions": {
       "deny": []
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

7. Skip any entries that already exist in the `deny` array.

8. Add the new entries to the `permissions.deny` array and write the file.

9. Confirm what was added and show the updated deny list.
