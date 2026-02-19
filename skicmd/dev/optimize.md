# /optimize

Analyzes and generates an optimization plan for the project or a specific scope.

## Parameters

- **$1** (optional): Scope — folder path, file path, or feature name. Default: entire project.
- **$2** (optional): Think level. Default: `megathink`. Options: `think` (~4K tokens), `megathink` (~10K tokens), `ultrathink` (~32K tokens).
- **$3** (optional): Model. Default: `Opus`. Options: `Opus`, `Sonnet`, `Haiku`.

## Usage

```
/optimize                             # optimize entire project, megathink, Opus
/optimize src/                        # optimize a specific folder
/optimize src/main.py                 # optimize a specific file
/optimize authentication              # optimize a feature by name
/optimize src/ ultrathink             # specific scope + think level
/optimize src/ megathink Sonnet       # specific scope + think level + model
```

## Instructions

1. Parse $1 (scope) from the user's input. If missing, default to the entire project.

2. Parse $2 (think level) from the user's input. Default: `megathink`. Optimization analysis benefits from deeper reasoning.

3. Parse $3 (model) from the user's input. Default: `Opus`.

4. **Determine scope type**:
   - **Folder path** (e.g. `src/`): scan all source files in the folder recursively.
   - **File path** (e.g. `src/main.py`): analyze the single file.
   - **Feature name** (e.g. `authentication`): search the codebase for related files (imports, class names, function names matching the feature) and collect them.
   - **Entire project** (default): scan the full project structure and source files.

5. Analyze the scoped code by prefixing the prompt with the think level keyword and using the specified model. Identify optimization opportunities in:
   - **Performance**: Slow algorithms, unnecessary loops, redundant computations, N+1 queries, missing caching.
   - **Code quality**: Duplicated logic, overly complex functions, dead code, inconsistent patterns.
   - **Resource usage**: Memory leaks, excessive file I/O, unmanaged connections, large imports.
   - **Architecture**: Tight coupling, missing abstractions, circular dependencies, poor separation of concerns.
   - **Maintainability**: Hard-coded values, missing error handling at boundaries, fragile patterns.

6. Generate an optimization plan including:
   - **Summary**: Overview of current state and key findings.
   - **Optimization items**: Ordered by impact (high → low), each with:
     - What to optimize and why
     - Files to modify
     - Concrete changes to make
     - Expected improvement
     - Risk level (low/medium/high)
   - **Quick wins**: Items that are low-effort, high-impact — do these first.
   - **Testing strategy**: How to verify optimizations don't break functionality.

7. Present the plan to the user for review.

8. After user approval (or edits), save the plan to `./doc/plan/` with the filename format: `opt_{scope}_{YYYY-MM-DD}.md` (use folder/feature name for scope, or `project` for entire project).

9. Confirm the saved path.

10. Ask the user if they want to run `/kickoff` to implement the optimization plan now.
