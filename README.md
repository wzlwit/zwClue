# zwClue

A personal library of reusable [Claude Code](https://claude.ai/code) hooks, skills, and commands. Acts as a remote registry — components are installed into other projects via the `/skicmd` command.

## Quick Start

Install a specific command into your project:

```
/skicmd repos/iniGit
```

Browse and install all available components:

```
/skicmd
```

## Available Components

### repos/ — Repository initialization

| Command | Description |
|---------|-------------|
| `/iniFolder` | Scaffold standard folder structure (src, tests, config, doc, scripts, assets) |
| `/iniGit` | Initialize git repo with .gitignore defaults and initial commit |
| `/iniPy` | Initialize Python project with conda env, pyproject.toml, and project scaffold |

### permi/ — Permission management

| Command | Description |
|---------|-------------|
| `/allow` | Add tool/app permissions to `.claude/settings.local.json` |
| `/deny` | Add tool/app denials to `.claude/settings.local.json` |

### dev/ — Development tools

| Command | Description |
|---------|-------------|
| `/addLaunch` | Create IDE launch/debug configs (VS Code, PyCharm) for ui, cmd, api, test |
| `/commit` | Stage, review, and commit changes in one workflow |
| `/debug` | Analyze and fix bugs in a file (default: active editor file) |
| `/dep` | Manage dependencies and environment (add, remove, sync, check) |
| `/doc` | Generate documentation (api, readme, changelog, file, folder) |
| `/env` | Manage environments (create, activate, remove, list, info) |
| `/iniClaude` | Generate CLAUDE.md for root, each subfolder, or all |
| `/launch` | Run the app using an existing launch configuration |
| `/listSC` | List all installed custom commands and skills |
| `/kickoff` | Implement code from an existing plan file |
| `/optimize` | Analyze and generate optimization plan for project or scope |
| `/refactor` | Analyze and generate refactoring plan for project or scope |
| `/planOn` | Generate implementation plan from a requirements file |
| `/pr` | Create a pull request on GitHub |
| `/push` | Push commits to remote with optional remote and branch |
| `/retry` | Re-run the last action from the conversation |
| `/review` | Review code changes before committing |
| `/test` | Run tests with auto-detected framework |
| `/troubleshoot` | Diagnose and fix errors from recent conversation actions |

### ui/ — UI development skills

| Skill | Description |
|-------|-------------|
| `pyqt6/` | PyQt6 desktop app development — widget templates, dialog templates, default stylesheet |

## Installing

The `/skicmd` installer supports multiple modes:

```
/skicmd                              # browse all components
/skicmd repos                        # all items in a category
/skicmd repos/iniGit                 # a specific component
/skicmd repos/iniGit https://...     # from a custom repo
```

Components are installed to `.claude/commands/` (project-level) or `~/.claude/commands/` (global), chosen at install time.

## Component Types

**Commands** — Single `.md` file with `## Instructions` for executable steps.

**Skills** — Folder with `SKILL.md` plus supporting files (templates, assets). Provides ongoing guidance for development workflows.

## Registry

`meta.md` in the repo root serves as the component registry. The `/skicmd` installer fetches it first to discover available components and construct precise download URLs without querying the full GitHub API tree.
