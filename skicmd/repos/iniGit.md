# /iniGit

Initializes a git repository in the current working directory with standard defaults.

## What It Does

1. Run `git init`
2. Create a `.gitignore` with common defaults
3. Create an initial commit

## .gitignore Defaults

```
# Dependencies
node_modules/
vendor/

# Environment
.env
.env.local
.env.*.local

# OS files
.DS_Store
Thumbs.db

# IDE
.vscode/
.idea/
*.swp
*.swo

# Build output
dist/
build/
out/

# Logs
*.log

# Claude Code (installed via /skicmd)
.claude/commands/skicmd.md
```

## Usage

Run `/iniGit` in any project root to initialize a git repo with sensible defaults.

## Instructions

1. Run `git init` in the current working directory
2. Create a `.gitignore` file with the defaults listed above
3. Create a `README.md` with the project name (current directory name) as the heading
4. Stage all files with `git add -A`
5. Create an initial commit with message: `Initial commit`

If git is already initialized (`.git/` exists):
1. Compare the existing `.gitignore` with the defaults above and list any missing entries.
2. Check if `README.md` exists.
3. Present the user with a list of updates available (missing .gitignore entries, missing README, etc.) and let them select which to apply.
4. If nothing needs updating, inform the user and stop.
