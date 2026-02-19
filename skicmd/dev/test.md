# /test

Runs tests for the current project.

## Parameters

- **$1** (optional): Test scope — file path, test name pattern, or folder. If omitted, run all tests.
- **$2** (optional): Test framework. Default: auto-detect.

## Usage

```
/test                                # run all tests
/test tests/test_main.py             # run a specific test file
/test tests/test_main.py::test_login # run a specific test function
/test tests/ pytest                  # run folder with specific framework
```

## Instructions

1. Parse $1 (scope) and $2 (framework) from the user's input.

2. **Auto-detect framework** if $2 is omitted:
   - If `pytest.ini`, `pyproject.toml` with `[tool.pytest]`, or `conftest.py` exists → `pytest`
   - If `package.json` with `test` script exists → `npm test`
   - If `Cargo.toml` exists → `cargo test`
   - If `go.mod` exists → `go test ./...`
   - If none detected, ask the user which framework to use.

3. **Build the test command** based on framework and scope:
   - **pytest**: `pytest {$1} -v` (or `pytest -v` for all)
   - **npm**: `npm test` (or `npm test -- {$1}`)
   - **cargo**: `cargo test {$1}`
   - **go**: `go test {$1}` (or `go test ./...` for all)

4. Run the test command and capture output.

5. **Parse results**: Extract pass/fail counts, failed test names, and error messages.

6. **Report**:
   - Total tests, passed, failed, skipped
   - For failures: test name, file/line, and error summary
   - If all passed, confirm success.

7. If tests failed, ask the user whether to:
   - **Debug** — run `/debug` on the failing test file
   - **Retry** — re-run only the failed tests
   - **Skip** — move on
