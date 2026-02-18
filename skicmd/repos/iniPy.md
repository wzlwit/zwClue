# /iniPy

Initializes a Python project in the current working directory with standard defaults.

## Parameters

- **$1** (optional): Python version (e.g. `3.12`). Default: latest LTS.
- **$2** (optional): Conda environment name. Default: current repo/directory name.

## Usage

```
/iniPy                      # latest LTS, env name = current dir name
/iniPy 3.11                 # targets Python 3.11
/iniPy 3.11 myenv           # targets Python 3.11, conda env "myenv"
```

## Instructions

1. Parse $1 from the user's input. If missing, look up the latest Python LTS version and use that.

2. Parse $2 from the user's input. If missing, use the current directory name as the conda environment name.

3. Create the conda environment: `conda create -n {$2} python={$1} -y`. If the environment already exists, warn the user and ask whether to recreate or skip.

4. Activate the new environment: `conda activate {$2}`. All subsequent commands should run inside this environment.

5. Create a `pyproject.toml` with:
   ```toml
   [project]
   name = "<current directory name>"
   version = "0.1.0"
   requires-python = ">={$1}"

   [build-system]
   requires = ["setuptools>=75.0"]
   build-backend = "setuptools.backends._legacy:_Backend"
   ```

5. Create a `.python-version` file containing the version from $1.

6. Create a `requirements.txt` (empty, with a comment header):
   ```
   # Project dependencies
   ```

7. Create a `src/__init__.py` (empty).

8. Create a `tests/__init__.py` (empty).

9. Create a `.gitignore` with Python-specific entries (append if it already exists):
   ```
   # Python
   __pycache__/
   *.py[cod]
   *.egg-info/
   dist/
   build/
   .venv/
   venv/
   .eggs/
   *.egg
   ```

11. Report what was created, the target Python version, and the conda environment name. Remind the user to run `conda activate {$2}` in new terminal sessions.
