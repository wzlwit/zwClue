# /allow

Adds a tool/app permission to `.claude/settings.local.json` in the current project.

## Parameters

- **$1** (required): The app or tool name to allow (e.g. `git`, `npm`, `docker`)
- **$2** (optional): Specific tool type to scope the permission to (e.g. `Bash`, `Read`, `Edit`). If omitted, allows across all tool types.

## Usage

```
/allow git                  # adds Bash(git:*), Read(git:*), Edit(git:*), Write(git:*)
/allow npm Bash             # adds only Bash(npm:*)
```

## Instructions

1. Parse $1 from the user's input. If missing, ask the user which tool to allow.

2. Parse $2 from the user's input. If missing, apply to all tool types: `Bash`, `Read`, `Edit`, `Write`.

3. Read `.claude/settings.local.json` in the current working directory. If it doesn't exist, create it with this structure:
   ```json
   {
     "permissions": {
       "allow": []
     }
   }
   ```

4. Construct the permission entries:
   - If $2 is provided: single entry `{$2}({$1}:*)`. Proceed to step 6.
   - If $2 is omitted: one entry per tool type — `Bash({$1}:*)`, `Read({$1}:*)`, `Edit({$1}:*)`, `Write({$1}:*)`.

5. If $2 was omitted (all tool types), show the list of entries that will be added and ask the user to confirm before proceeding.

6. Skip any entries that already exist in the `allow` array.

7. Add the new entries to the `permissions.allow` array and write the file.

8. Confirm what was added and show the updated allow list.
