# /kickoff

Implements code from an existing plan file.

## Parameters

- **$1** (optional): Path to plan file. If omitted, search `./doc/plan/` for the most recent plan file.
- **$2** (optional): Think level. Default: `think`. Options: `think` (~4K tokens), `megathink` (~10K tokens), `ultrathink` (~32K tokens).
- **$3** (optional): Model. Default: `Opus`. Options: `Opus`, `Sonnet`, `Haiku`.

## Usage

```
/kickoff                                              # use latest plan
/kickoff doc/plan/plan_requirements_2026-02-18.md     # specific plan
/kickoff doc/plan/plan_requirements_2026-02-18.md megathink Sonnet
```

## Instructions

1. Parse $1 from the user's input. If missing:
   a. Search `./doc/plan/` for files with `plan` in the filename.
   b. If multiple matches, sort by date (newest first) and pick the most recent.
   c. If no matches, ask the user to provide the file path or run `/planOn` first.

2. Parse $2 (think level) from the user's input. Default: `think`. Implementation is step-by-step execution from an existing plan, so standard think is efficient — escalate to megathink/ultrathink for complex steps.

3. Parse $3 (model) from the user's input. Default: `Opus`.

4. Read the plan file in full.

5. Parse the implementation steps from the plan. For each step, extract:
   - Files to create or modify
   - Key logic or dependencies
   - Order and dependencies on other steps

6. Present the implementation steps to the user as a numbered checklist. Prompt the user to choose a mode (auto-select after 60 seconds):
   - **Auto** (default) — implement all steps without pausing. Fastest execution.
   - **Step-by-step** — confirm each step before proceeding. Pause after each step for user to approve or skip, then continue.
   - **Review** — show the diff/changes for each step before applying. User confirms or rejects each change, then continue to the next step.

7. For each approved step, prefix the prompt with the think level keyword and use the specified model to:
   a. Create or modify the files as described in the plan.
   b. Follow existing code conventions and patterns in the project.
   c. In **Step-by-step** mode: show what will be done and wait for confirmation before executing.
   d. In **Review** mode: generate the changes, show the diff, and wait for user to accept or reject before writing.
   e. Mark the step as done after completion.

8. After each step, run any relevant tests or validation if described in the plan's testing strategy.

9. After all steps are complete, present a summary:
   - Steps completed
   - Files created or modified
   - Any steps skipped or failed
   - Suggested next actions (run tests, review, commit)
