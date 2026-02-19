# /refactor

Analyzes and generates a refactoring plan for the specified scope.

## Parameters

- **$1** (optional): Scope — folder path, file path, or feature name. Default: entire project.
- **$2** (optional): Think level. Default: `megathink`. Options: `think` (~4K tokens), `megathink` (~10K tokens), `ultrathink` (~32K tokens).
- **$3** (optional): Model. Default: `Opus`. Options: `Opus`, `Sonnet`, `Haiku`.

## Usage

```
/refactor                             # refactor entire project, megathink, Opus
/refactor src/                        # refactor a specific folder
/refactor src/main.py                 # refactor a specific file
/refactor authentication              # refactor a feature by name
/refactor src/ ultrathink             # specific scope + think level
/refactor src/ megathink Sonnet       # specific scope + think level + model
```

## Instructions

1. Parse $1 (scope) from the user's input. If missing, default to the entire project.

2. Parse $2 (think level) from the user's input. Default: `megathink`.

3. Parse $3 (model) from the user's input. Default: `Opus`.

4. **Determine scope type**:
   - **Folder path** (e.g. `src/`): scan all source files in the folder recursively.
   - **File path** (e.g. `src/main.py`): analyze the single file.
   - **Feature name** (e.g. `authentication`): search the codebase for related files (imports, class names, function names matching the feature) and collect them.
   - **Entire project** (default): scan the full project structure and source files.

5. Analyze the scoped code by prefixing the prompt with the think level keyword and using the specified model. Identify refactoring opportunities in:
   - **Structure**: Extract method/class, move to appropriate module, split large files.
   - **Duplication**: Repeated logic that should be consolidated into shared functions or base classes.
   - **Naming**: Unclear variable/function/class names that hurt readability.
   - **Complexity**: Long methods, deep nesting, complex conditionals that can be simplified.
   - **Patterns**: Inconsistent patterns across the codebase that should be unified.
   - **Dependencies**: Circular imports, tight coupling, missing interfaces or abstractions.
   - **Dead code**: Unused imports, unreachable branches, deprecated functions.

6. Generate a refactoring plan including:
   - **Summary**: Overview of current code quality and key findings.
   - **Refactoring items**: Ordered by impact (high → low), each with:
     - What to refactor and why
     - Files to modify
     - Concrete changes to make
     - Risk level (low/medium/high)
   - **Safe refactors**: Items that are low-risk, behavior-preserving — do these first.
   - **Testing strategy**: How to verify refactors don't break functionality.

7. Present the plan to the user for review.

8. After user approval (or edits), save the plan to `./doc/plan/` with the filename format: `refactor_{scope}_{YYYY-MM-DD}.md` (use folder/feature name for scope, or `project` for entire project).

9. Confirm the saved path.

10. Ask the user if they want to run `/kickoff` to implement the refactoring plan now.
