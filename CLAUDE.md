# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Purpose

A personal library of reusable Claude Code **hooks**, **skills**, and **commands**. The repo acts as a remote registry — components are installed into other projects via the `/skicmd` command.

## Repository Layout

- `meta.md` — Component registry. Lists all installable components and their paths. Fetched first by `/skicmd` to discover available components.
- `skicmd/<category>/` — Source skill/command definitions, organized by category (e.g. `skicmd/repos/`). These are the installable components.
- `.claude/commands/` — Repo-internal slash commands (e.g. `/skicmd` installer). Excluded from remote install listings.
- `.claude/skills/` — Repo-internal skills. Excluded from remote install listings.

When adding or removing components under `skicmd/`, keep `meta.md` in sync.

## Component Types

**Commands** (single file): A `.md` file directly in a category folder.
- Filename becomes the command name (e.g. `iniGit.md` → `/iniGit`)
- Starts with `# /commandName` heading
- Includes `## Instructions` section with self-contained, executable steps
- Parameters are documented with `$1`, `$2` notation

**Skills** (folder): A subfolder containing `SKILL.md` plus supporting files (templates, assets, etc.).
- `SKILL.md` defines conventions and guidance for ongoing development
- Subfolders hold reusable templates, stylesheets, and other assets
- Example: `skicmd/ui/pyqt6/` with `SKILL.md`, `widgets/`, `dialogs/`, `resources/`

## Installing Components

Run `/skicmd` (defined in `.claude/commands/skicmd.md`) to download and install components from this repo into a target project. Default source: `https://github.com/wzlwit/zwClue`.

- `/skicmd` — browse and install all components from the repo
- `/skicmd repos` or `/skicmd repos/` — install all items in a category folder
- `/skicmd repos/iniGit` — install a specific component
- `/skicmd repos/iniGit https://github.com/user/repo` — install from a custom repo

Components are installed to `.claude/commands/` (project) or `~/.claude/commands/` (global), chosen at install time.