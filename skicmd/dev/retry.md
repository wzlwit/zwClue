# /retry

Lists recent actions from the conversation and re-tries the latest failed one, or a selected action.

## Parameters

- **$1** (optional): Action number from the list to retry. If omitted, auto-retry the latest action with an error after 10 seconds.

## Usage

```
/retry                   # list actions, auto-retry latest error after 10s
/retry 3                 # retry action #3 from the list
```

## Instructions

1. Scan the current conversation and compile a numbered list of recent actions taken (commands, file edits, file creations, tool calls, code runs). For each action show:
   - **#** — action number
   - **Title** — short description of the action (e.g. "Write src/main.py", "Run pytest")
   - **Status** — success or failed
   - **Error** — if failed, show error keywords or first line of the error message

2. Present the list to the user.

3. **If $1 is provided**: retry the specified action by number.

4. **If $1 is omitted**: identify the most recent action with an error. If found:
   - Inform the user it will auto-retry in 10 seconds.
   - Wait 10 seconds, then re-run the failed action.
   - If no errors found, inform the user all actions succeeded and stop.

5. Re-run the selected action exactly as before.

6. If the action was a multi-step operation, re-run the entire sequence.

7. Report the result, whether it succeeded or failed again, and any differences from the previous attempt.
