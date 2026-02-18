# /retry

Re-runs the last action or command that was executed in the current conversation.

## Parameters

None.

## Usage

```
/retry
```

## Instructions

1. Look back in the current conversation to identify the most recent action taken (e.g. a command execution, file edit, file creation, tool call, or code run).

2. If the last action failed, re-run it exactly as before.

3. If the last action succeeded but produced unexpected results, re-run it and compare the output.

4. If the last action was a multi-step operation, re-run the entire sequence from the first step.

5. Report the result and whether it differs from the previous attempt.
