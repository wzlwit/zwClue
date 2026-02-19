# /env

Manages project environments (conda, venv).

## Parameters

- **$1** (optional): Action — `info`, `create`, `activate`, `remove`, `list`. Default: `info`.
- **$2** (optional): Environment name for `create`/`activate`/`remove`. Default: current directory name.

## Usage

```
/env                             # show current environment info
/env list                        # list all available environments
/env create myenv                # create a new conda env
/env activate myenv              # activate an environment
/env remove myenv                # remove an environment
```

## Instructions

1. Parse $1 (action) and $2 (env name) from the user's input. Default action: `info`.

2. **Detect environment type**:
   - Check for active conda env: `conda info --envs`
   - Check for `venv/` or `.venv/` directory
   - Check `.python-version` file for expected Python version

3. **Actions**:

   **info** — Show current environment details:
   - Active environment name and type (conda/venv/system)
   - Python version: `python --version`
   - Environment path
   - Number of installed packages: `pip list | wc -l`
   - Whether it matches `.python-version` if present

   **list** — List all available environments:
   - Conda: `conda env list`
   - venv: check for `venv/`, `.venv/` in current and parent directories
   - Mark the currently active one

   **create** — Create a new environment:
   - Use $2 as the name (default: current directory name)
   - Check `.python-version` for the target Python version, otherwise ask
   - Conda: `conda create -n {$2} python={version} -y`
   - venv: `python -m venv {$2}`
   - Activate after creation
   - Report the new environment details

   **activate** — Activate an environment:
   - Conda: `conda activate {$2}`
   - venv: `source {$2}/bin/activate` (Unix) or `{$2}\Scripts\activate` (Windows)
   - If $2 not found, show available environments and ask the user to pick

   **remove** — Remove an environment:
   - Show the environment details and ask for confirmation
   - Conda: `conda env remove -n {$2} -y`
   - venv: remove the directory
   - Warn if it's the currently active environment

4. After any action, confirm the result and show the current active environment.
