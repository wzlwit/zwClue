# /planOff

Implements code from an existing plan file.

## Parameters

- **$1** (optional): Path to plan file. If omitted, search `./doc/plan/` for the most recent plan file.
- **$2** (optional): Think level. Default: `Think more`. Options: `Think`, `Think more`, `Think hard`, `Ultrathink`.
- **$3** (optional): Model. Default: `Opus`. Options: `Opus`, `Sonnet`, `Haiku`.

## Usage

```
/planOff                                              # use latest plan
/planOff doc/plan/plan_requirements_2026-02-18.md     # specific plan
/planOff doc/plan/plan_requirements_2026-02-18.md "Think hard" Sonnet
```

## Instructions

1. Parse $1 from the user's input. If missing:
   a. Search `./doc/plan/` for files with `plan` in the filename.
   b. If multiple matches, sort by date (newest first) and pick the most recent.
   c. If no matches, ask the user to provide the file path or run `/planOn` first.

2. Parse $2 (think level) from the user's input. Default: `Think more`.

3. Parse $3 (model) from the user's input. Default: `Opus`.

4. Read the plan file in full.

5. Parse the implementation steps from the plan. For each step, extract:
   - Files to create or modify
   - Key logic or dependencies
   - Order and dependencies on other steps

6. Present the implementation steps to the user as a numbered checklist. Ask the user to confirm:
   - **All** — implement all steps in order
   - **Select** — pick specific steps to implement
   - **Cancel** — abort

7. For each approved step, prefix the prompt with the think level keyword and use the specified model to:
   a. Create or modify the files as described in the plan.
   b. Follow existing code conventions and patterns in the project.
   c. Mark the step as done after completion.

8. After each step, run any relevant tests or validation if described in the plan's testing strategy.

9. After all steps are complete, present a summary:
   - Steps completed
   - Files created or modified
   - Any steps skipped or failed
   - Suggested next actions (run tests, review, commit)
