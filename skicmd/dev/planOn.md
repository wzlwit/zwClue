# /planOn

Reads a requirements file and generates an implementation plan.

## Parameters

- **$1** (optional): Path to requirements file. If omitted, search `./doc/` for files with "require" in the name.
- **$2** (optional): Think level. Default: `Think more`. Options: `Think`, `Think more`, `Think hard`, `Ultrathink`.
- **$3** (optional): Model. Default: `Opus`. Options: `Opus`, `Sonnet`, `Haiku`.

## Usage

```
/planOn                                          # auto-find requirements, Think more, Opus
/planOn doc/requirements.md                      # specific file
/planOn doc/requirements.md "Think hard"         # specific file + think level
/planOn doc/requirements.md "Think hard" Sonnet  # specific file + think level + model
```

## Instructions

1. Parse $1 from the user's input. If missing:
   a. Search `./doc/` recursively for files with `require` in the filename (case-insensitive).
   b. If multiple matches, present the list and ask the user to pick one.
   c. If no matches, ask the user to provide the file path.

2. Parse $2 (think level) from the user's input. Default: `Think more`.

3. Parse $3 (model) from the user's input. Default: `Opus`.

4. Read the requirements file in full.

5. Generate an implementation plan by prefixing the prompt with the think level keyword and using the specified model. The plan should include:
   - **Context**: What problem the requirements address and the intended outcome.
   - **Architecture**: High-level design decisions, component breakdown, and data flow.
   - **Implementation steps**: Ordered list of concrete tasks, each with:
     - Files to create or modify
     - Key logic or algorithms
     - Dependencies on other steps
   - **Testing strategy**: How to verify each component works.
   - **Risks and open questions**: Anything unclear or potentially problematic.

6. Present the plan to the user for review.

7. After user approval (or edits), save the plan to `./doc/plan/` with the filename format: `plan_{original_filename}_{YYYY-MM-DD}.md`.

8. Confirm the saved path.
