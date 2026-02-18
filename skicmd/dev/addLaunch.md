# /addLaunch

Creates a launch/debug configuration file so developers can run and test the project from their IDE.

## Parameters

- **$1** (optional): Scope of the launch config. Examples: `ui`, `cmd`, `api`, `test`. If omitted, ask the user what they want to launch.
- **$2** (optional): IDE to target. Default: `vscode`.

## Usage

```
/addLaunch ui                # VS Code launch.json for a PyQt6/UI app
/addLaunch cmd               # VS Code launch.json for a CLI/script
/addLaunch test              # VS Code launch.json for running tests
/addLaunch ui pycharm        # PyCharm run config for a UI app
```

## Instructions

1. Parse $1 from the user's input. If missing, ask the user what type of application to launch (`ui`, `cmd`, `api`, `test`).

2. Parse $2 from the user's input. If missing, default to `vscode`.

3. Inspect the project to determine the entry point:
   - Look for `src/main.py`, `main.py`, `app.py`, or `src/app.py`
   - If not found, ask the user for the entry point file path.

4. **For VS Code** ($2 = `vscode`):
   a. Create `.vscode/launch.json` if it doesn't exist. If it exists, append to the `configurations` array.
   b. Generate the configuration based on $1 scope:

   **ui** — Launch a GUI application:
   ```json
   {
     "name": "Launch UI",
     "type": "debugpy",
     "request": "launch",
     "program": "${workspaceFolder}/src/main.py",
     "console": "integratedTerminal",
     "justMyCode": true
   }
   ```

   **cmd** — Launch a CLI script:
   ```json
   {
     "name": "Launch CMD",
     "type": "debugpy",
     "request": "launch",
     "program": "${workspaceFolder}/src/main.py",
     "console": "integratedTerminal",
     "args": [],
     "justMyCode": true
   }
   ```

   **api** — Launch an API server:
   ```json
   {
     "name": "Launch API",
     "type": "debugpy",
     "request": "launch",
     "program": "${workspaceFolder}/src/main.py",
     "console": "integratedTerminal",
     "justMyCode": true,
     "env": {
       "PYTHONDONTWRITEBYTECODE": "1"
     }
   }
   ```

   **test** — Run tests with debugger:
   ```json
   {
     "name": "Run Tests",
     "type": "debugpy",
     "request": "launch",
     "module": "pytest",
     "args": ["tests/", "-v"],
     "console": "integratedTerminal",
     "justMyCode": true
   }
   ```

5. **For PyCharm** ($2 = `pycharm`):
   a. Create `.idea/runConfigurations/` directory if it doesn't exist.
   b. Generate an XML run configuration file based on $1 scope with the appropriate entry point and working directory.

6. If a launch config with the same name already exists, warn the user and ask to overwrite or rename.

7. Report what was created and how to use it (e.g. "Press F5 in VS Code to launch").
