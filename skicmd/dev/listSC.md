# /listSC

Lists all custom commands and skills installed in the current project and globally.

## Parameters

- **$1** (optional): Scope — `project`, `global`, `all`. Default: `all`.

## Usage

```
/listSC                          # list all commands and skills (project + global)
/listSC project                  # list project-level only
/listSC global                   # list global only
```

## Instructions

1. Parse $1 (scope) from the user's input. Default scope: `all`.

2. **Scan for installed components**:

   **project** — scan the current project:
   - Commands: `.claude/commands/*.md`
   - Skills: `.claude/skills/*/SKILL.md`

   **global** — scan the global location:
   - Commands: `~/.claude/commands/*.md`
   - Skills: `~/.claude/skills/*/SKILL.md`

   **all** — scan both project and global.

3. For each component found, extract:
   - Name (filename without `.md`, or folder name for skills).
   - First line description (from the `# /name` heading or the line after it).
   - Type: command or skill.

4. Display results grouped by location and type:

   ```
   Project commands:
     /commit    — Stage, review, and commit changes
     /push      — Push commits to remote
     ...

   Project skills:
     pyqt6/     — PyQt6 desktop app development
     ...

   Global commands:
     /skicmd    — Install components from zwClue
     ...
   ```

5. Show total counts: `X project commands, Y project skills, Z global commands, W global skills`.

6. If no components found in a scope, report it (e.g. "No project commands found").
