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
1. Read the existing `.gitignore` file (or note it's missing).
2. Check each entry from the `.gitignore Defaults` section above line by line. An entry is missing if the exact line does not appear in the existing `.gitignore`. Entries to check:
   - `node_modules/`, `vendor/`
   - `.env`, `.env.local`, `.env.*.local`
   - `.DS_Store`, `Thumbs.db`
   - `.vscode/`, `.idea/`, `*.swp`, `*.swo`
   - `dist/`, `build/`, `out/`
   - `*.log`
   - `.claude/commands/skicmd.md`
3. Check if `README.md` exists.
4. Present the user with a numbered list of all missing items and let them select which to apply (all or specific ones).
5. Append selected entries to `.gitignore` (with section comments). Create missing files.
6. If nothing needs updating, inform the user and stop.
