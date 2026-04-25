# Phase 1: Environment Setup

Get your development environment running so you can work on the FastAPI Workshop.

## Step: Install prerequisites

You need Git and `uv` installed on your machine. `uv` manages Python and all project dependencies — no separate Python install required.

### collapsible: macOS [default-on-macOS]

```bash
# Install Homebrew if you don't have it
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install Git and uv
brew install git
brew install uv
```

### collapsible: Windows [default-on-Windows]

1. Install [Git for Windows](https://git-scm.com/download/win)
2. Install `uv` via PowerShell:

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

Open a new terminal (PowerShell or Git Bash) after installation so the `uv` command is available.

### collapsible: Linux [default-on-Linux]

```bash
# Ubuntu/Debian
sudo apt update && sudo apt install -y git

# Install uv
curl -LsSf https://astral.sh/uv/install.sh | sh
```

> Restart your terminal (or run `source $HOME/.local/bin/env`) after installing `uv`.

Verify your setup:

```bash
git --version
uv --version
```

## Step: Install dependencies

`uv` creates the virtual environment and installs everything in one command:

```bash
uv sync --extra all
```

This will:
- Create a `.venv` virtual environment automatically
- Install FastAPI in editable mode (source changes take effect immediately, no reinstall needed)
- Install all development and test dependencies

## Step: Verify everything works

Run the test suite to confirm your setup is working:

```bash
bash scripts/test.sh
```

You should see output ending with something like:

```
===== N passed in Xs =====
```

> **Note:** Some tests may fail — that's expected! The pre-seeded bugs are already in the code. Your goal is to find and fix them.

You can also run a single test to do a quick sanity check:

```bash
PYTHONPATH=./docs_src pytest tests/test_application.py -v
```

- [ ] Git installed and working
- [ ] `uv` installed and working
- [ ] Repository cloned
- [ ] `uv sync --extra all` succeeds
- [ ] `bash scripts/test.sh` runs without setup errors

## Footer

- [uv Documentation](https://docs.astral.sh/uv/)
- [Git Installation Guide](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [FastAPI Contributing Guide](https://fastapi.tiangolo.com/contributing/)
- [Architecture Overview](../CLAUDE.md)
