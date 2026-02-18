# /debug

Analyzes and fixes bugs in a specified file or the currently active editor file.

## Parameters

- **$1** (optional): File path to debug. Default: the currently active/open file in the editor.

## Usage

```
/debug                           # debug the active file
/debug src/main.py               # debug a specific file
/debug src/widgets/my_widget.py  # debug a specific widget
```

## Instructions

1. Parse $1 from the user's input. If missing, use the currently active/open file in the editor.

2. Read the target file in full.

3. **Check for IDE diagnostics**: Query the editor/IDE for any reported errors, warnings, or linting issues on the file.

4. **Static analysis**: Review the code for:
   - Syntax errors
   - Undefined variables or missing imports
   - Type mismatches or incorrect function signatures
   - Unreachable code or logic errors
   - Off-by-one errors, incorrect conditions
   - Resource leaks (unclosed files, connections)
   - Unhandled exceptions in critical paths

5. **Run the file** (if executable): Attempt to run or import the file to surface runtime errors:
   - For Python: `python -c "import {module}"` or `python {file}`
   - Capture any tracebacks or error output

6. **Run related tests**: Look for test files matching the target (e.g. `src/foo.py` → `tests/test_foo.py`). If found, run them to identify failing assertions.

7. **Present findings**: List all identified bugs ranked by severity:
   - **Error**: Will cause crashes or incorrect behavior
   - **Warning**: Potential issues or bad practices
   - For each bug, show the line number, the issue, and the proposed fix

8. **Apply fixes**: Ask the user which fixes to apply (all, specific ones, or none). Apply the approved fixes and re-run validation (step 5–6) to confirm they resolve the issues.

9. **Report**: Summarize what was found and fixed.
