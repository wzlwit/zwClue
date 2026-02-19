# /dep

Manages project dependencies and environment.

## Parameters

- **$1** (optional): Action — `add`, `remove`, `list`, `sync`, `check`. Default: `list`.
- **$2** (optional): Package name(s) for `add`/`remove`. Multiple packages separated by spaces.

## Usage

```
/dep                             # list all installed dependencies
/dep add requests flask          # add packages
/dep remove flask                # remove a package
/dep sync                        # install all from requirements file
/dep check                       # check for outdated/missing packages
```

## Instructions

1. Parse $1 (action) and $2 (packages) from the user's input. Default action: `list`.

2. **Detect the environment and package manager**:
   - Check for active conda env: `conda info --envs` — identify the active one.
   - Check for `venv/` or `.venv/` directory.
   - Detect package manager from project files:
     - `requirements.txt` or `pyproject.toml` → `pip`
     - `package.json` → `npm`/`yarn`/`pnpm` (check lock files)
     - `Cargo.toml` → `cargo`
     - `go.mod` → `go`
   - If no env detected, warn the user and ask whether to create one or proceed globally.

3. **Actions**:

   **list** — Show installed dependencies:
   - Python: `pip list`
   - Node: `npm list --depth=0`
   - Report the active environment name.

   **add** — Install and record packages:
   - Python: `pip install {$2}`, then add to `requirements.txt` (or `pyproject.toml` dependencies).
   - Node: `npm install {$2}`, auto-updates `package.json`.
   - Confirm what was added.

   **remove** — Uninstall and remove from records:
   - Python: `pip uninstall {$2} -y`, then remove from `requirements.txt`.
   - Node: `npm uninstall {$2}`, auto-updates `package.json`.
   - Confirm what was removed.

   **sync** — Install all dependencies from the requirements file:
   - Python: `pip install -r requirements.txt` (or `pip install -e .` for pyproject.toml).
   - Node: `npm install`.
   - Report any failures.

   **check** — Audit dependencies:
   - **Outdated**: `pip list --outdated` / `npm outdated`
   - **Missing**: Compare requirements file against installed packages.
   - **Unused**: Check imports in `src/` against installed packages (Python only).
   - Present findings and ask the user which to fix.

4. After any action, show a summary of the current environment state (env name, package count, any warnings).
