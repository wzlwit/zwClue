# /doc

Generates documentation for the current project.

## Parameters

- **$1** (optional): Scope — file path, folder, or doc type (`api`, `readme`, `changelog`, `all`). Default: `all`.
- **$2** (optional): Output folder. Default: `./doc/dev/`.

## Usage

```
/doc                             # generate all docs to ./doc/dev/
/doc src/main.py                 # generate docs for a specific file
/doc src/                        # generate docs for all files in src/
/doc api                         # generate API documentation
/doc readme                      # generate/update README.md
/doc changelog                   # generate CHANGELOG.md from git history
/doc all ./docs                  # generate all docs to custom folder
```

## Instructions

1. Parse $1 (scope) and $2 (output folder) from the user's input. Default scope: `all`. Default output: `./doc/dev/`.

2. Create the output folder if it doesn't exist (`mkdir -p`).

3. **Determine scope**:

   **File path** (e.g. `src/main.py`) — document a single file:
   - Read the file and analyze classes, functions, and module structure.
   - Generate a markdown doc with: module overview, class/function signatures, parameters, return types, and usage examples.
   - If `{$2}/{filename}.md` already exists, show what changed and ask to overwrite or merge.
   - Save to `{$2}/{filename}.md`.

   **Folder** (e.g. `src/`) — document all files in the folder:
   - Scan for source files recursively.
   - Generate a doc per file plus an index page linking them all.
   - For existing docs, show what changed and ask to overwrite or merge.
   - Save to `{$2}/`.

   **api** — generate API documentation:
   - Scan `src/` for classes, public methods, endpoints, and interfaces.
   - Generate structured API reference with signatures, parameters, and return types.
   - If `{$2}/api.md` already exists, show what changed and ask to overwrite or merge.
   - Save to `{$2}/api.md`.

   **readme** — generate or update `README.md`:
   - Analyze project structure, entry points, dependencies, and existing docs.
   - Generate/update README with: project description, setup instructions, usage, and project structure.
   - Save to `./README.md` (project root).

   **changelog** — generate or update `CHANGELOG.md` from git history:
   - Run `git log --oneline --no-merges` to get commit history.
   - Group commits by date or tag.
   - Generate a changelog in Keep a Changelog format.
   - If `./CHANGELOG.md` already exists, append new entries since last documented date/tag.
   - Save to `./CHANGELOG.md` (project root).

   **all** — generate everything:
   - Run api, then folder docs for `src/`.
   - Ask the user if they also want readme and changelog updated.

4. For each generated doc, show the user a preview of the first 10 lines.

5. Ask the user to confirm or edit before saving.

6. Report all files created/updated and their paths.
