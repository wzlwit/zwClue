# /launch

Launches the application using an existing launch configuration.

## Parameters

- **$1** (optional): Launch config name to run (e.g. `ui`, `cmd`, `api`, `test`). If omitted, list available configs and ask the user to pick one.

## Usage

```
/launch                  # list available configs and pick one
/launch ui               # run the "Launch UI" config
/launch test             # run the "Run Tests" config
```

## Instructions

1. Parse $1 from the user's input.

2. Look for an existing launch configuration:
   - Check `.vscode/launch.json` for VS Code configs.
   - Check `.idea/runConfigurations/` for PyCharm configs.
   - If no launch config file is found, tell the user to run `/addLaunch` first and stop.

3. **If $1 is missing**: List all available configurations by name and ask the user which one to run.

4. **If $1 is provided**: Match $1 against configuration names (case-insensitive, partial match — e.g. `ui` matches `Launch UI`, `test` matches `Run Tests`). If no match, show available configs and ask the user to pick.

5. Extract the run command from the matched configuration:
   - If `program` is set: `python {program}`
   - If `module` is set: `python -m {module}` with any `args`
   - Include any `env` variables as environment prefixes
   - Include any `args`

6. Run the command in the terminal and show the output.
