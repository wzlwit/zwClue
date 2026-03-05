# /iniFolder

Initializes a standard folder structure in the current working directory.

## Created Structure

```
./src/
./tests/
./config/
./docs/
  plans/
  dev/
./scripts/
./assets/
```

## Usage

Run `/iniFolder` in any project root to scaffold the standard directory layout.

## Instructions

Create the following folder structure in the current working directory:

- `src/` — source code
- `tests/` — test files
- `config/` — configuration files
- `docs/` — project documentation root
  - `docs/plans/` — planning documents
  - `docs/dev/` — development documents
- `scripts/` — build, deploy, and utility scripts
- `assets/` — static assets (images, fonts, etc.)

Use `mkdir -p` to create all directories. Add a `.gitkeep` file in each leaf directory so git tracks them.

Create a `README.md` with the project name (current directory name) as the heading.

Report what was created when done.
