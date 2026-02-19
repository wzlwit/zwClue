# /iniClaude

Generates `CLAUDE.md` files by invoking the `/init` command at the specified level.

## Parameters

- **$1** (optional): Level — `root`, `all`, `each`. Default: `all`.

## Usage

```
/iniClaude                       # generate CLAUDE.md for all (subfolders then root)
/iniClaude root                  # generate CLAUDE.md for root folder only
/iniClaude each                  # generate CLAUDE.md for each subfolder only
/iniClaude all                   # generate CLAUDE.md for all (subfolders then root)
```

## Instructions

1. Parse $1 (level) from the user's input. Default level: `all`.

2. Scan the project to identify target folders:

   **root** — root folder only:
   - Target: `./` (project root).

   **each** — each subfolder only:
   - Scan for immediate subdirectories under `./` that contain source files.
   - Exclude: `node_modules`, `venv`, `.venv`, `__pycache__`, `.git`, `.claude`, `doc`, `assets`, `build`, `dist`, `.tox`, `.mypy_cache`.
   - List the discovered subfolders and ask the user to confirm or deselect any.

   **all** — each subfolder first, then root:
   - Run `each` first so every subfolder has its own `CLAUDE.md`.
   - Then run `root` — since subfolders already have detailed docs, the root `CLAUDE.md` should be concise: high-level architecture, cross-module relationships, and project-wide conventions only. Do not repeat subfolder details.

3. For each target folder, invoke `/init` scoped to that folder:
   - Analyze the folder's code, structure, and purpose.
   - Generate a `CLAUDE.md` in that folder.
   - If `CLAUDE.md` already exists in the target folder, show what changed and ask to overwrite or merge.

4. After all folders are processed, report:
   - List of all `CLAUDE.md` files created or updated.
   - Any folders that were skipped and why.
