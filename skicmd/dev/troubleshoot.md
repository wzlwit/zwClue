# /troubleshoot

Analyzes errors from recent actions in the current conversation and attempts to diagnose and fix them.

## Parameters

- **$1** (optional): Specific error message or keyword to focus on. If omitted, scan the most recent action/response for errors.

## Usage

```
/troubleshoot                        # check the last action for errors
/troubleshoot ModuleNotFoundError    # focus on a specific error type
/troubleshoot "permission denied"    # focus on a specific message
```

## Instructions

1. Parse $1 from the user's input. If provided, use it to narrow the diagnosis.

2. **Identify the error**: Look at the most recent conversation context for:
   - Command exit codes (non-zero)
   - Python tracebacks or exceptions
   - Permission denied errors
   - File not found errors
   - Dependency/import errors
   - Build or compilation failures
   - Git errors
   - Network/connection errors

3. **Gather context**: For the identified error, collect:
   - The exact error message and traceback
   - The command or action that triggered it
   - Relevant file paths mentioned in the error
   - Current working directory and environment (conda env, Python version)

4. **Diagnose**: Based on the error type, check common causes:
   - **ModuleNotFoundError / ImportError**: Check if the package is in `requirements.txt`, check active conda env with `conda info --envs`, check if installed with `pip list | grep {module}`
   - **PermissionError**: Check file permissions, check if file is locked or in use
   - **FileNotFoundError**: Verify the path exists, check for typos, check working directory
   - **SyntaxError / IndentationError**: Read the file at the reported line, check for obvious issues
   - **Git errors**: Check `git status`, check for merge conflicts, check remote connectivity
   - **Connection errors**: Check network, check URL validity, check authentication

5. **Propose a fix**: Present the root cause and a concrete fix. If confident, ask the user if they want to apply the fix. If uncertain, present multiple possible causes ranked by likelihood.

6. **Apply fix** (if user approves): Execute the fix and verify it resolves the error by re-running the original command.

7. **Report**: Summarize what went wrong, what was fixed, and any preventive steps.
