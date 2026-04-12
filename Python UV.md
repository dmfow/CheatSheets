## UV
UV is Python package and project manager (virtual environment), written in Rust.
<br>
<br>
Self claimed: A single tool to replace pip, pip-tools, pipx, poetry, pyenv, twine, virtualenv, and more.
10-100x faster than pip
<br> Read more at:
<br>
https://docs.astral.sh/uv/

#### From
```
This page cheat sheet is close to
https://gist.github.com/rollingmountains
```

## Project Handling

#### Initialize New Project
```bash
uv init myproject
cd myproject
```

#### Initialize in Current Directory
```bash
uv init
```

#### Initialize with Specific Python Version
```bash
uv init --python 3.11
```

## Virtual Environment Management

#### Create Virtual Environment
```bash
uv venv                    # Create .venv in current directory
uv venv myenv             # Create named environment
uv venv --python 3.11     # Specify Python version
```

#### List Virtual Environments
```bash
ls -la                     # Show .venv in current directory
find ~ -name ".venv" -type d 2>/dev/null  # Find all .venv directories
uv venv list              # List UV managed environments (if available)
```

#### Find Virtual Environment Location
```bash
echo $VIRTUAL_ENV         # Show active venv path
which python              # Show active Python executable path
python -c "import sys; print(sys.prefix)"  # Show Python environment prefix
pwd                       # Current directory (where .venv usually is)
```

#### Check Virtual Environment Status
```bash
echo $VIRTUAL_ENV         # Shows path if venv is active
ps1                       # Check if prompt shows venv name
python --version          # Check Python version in current env
```

#### Activate Virtual Environment
```bash
source .venv/bin/activate
```

#### Deactivate Virtual Environment
```bash
deactivate               # Exit virtual environment
```

#### Create and Use Environment in One Step
```bash
uv run python script.py   # Auto-creates venv if needed
```

## Package Management

#### Install Packages
```bash
uv add requests            # Add package to project
uv add "django>=4.0"      # Add with version constraint
uv add --dev pytest       # Add as development dependency
uv add --optional test pytest  # Add to optional group
```

#### Remove Packages
```bash
uv remove requests         # Remove package
uv remove --dev pytest    # Remove dev dependency
```

#### Install from Requirements
```bash
uv pip install -r requirements.txt
uv sync                    # Install all project dependencies
```

#### Upgrade Packages
```bash
uv lock --upgrade          # Update lock file
uv sync                    # Sync to updated versions
```

## Environment Checks & Info

#### Check Virtual Environment Status
```bash
which python              # Shows active Python path
echo $VIRTUAL_ENV         # Shows active venv path
uv python list           # List available Python versions
```

#### Environment Information
```bash
uv info                   # Show UV configuration
uv python find 3.11      # Find specific Python version
uv tree                  # Show dependency tree
```

#### List Installed Packages
```bash
uv pip list               # List packages in current env
uv pip show package_name  # Show package details
```

#### Check Project Status
```bash
uv status                 # Show project sync status  
uv check                  # Validate project dependencies
```

## Python Version Management

#### Install Python Versions
```bash
uv python install 3.11   # Install Python 3.11
uv python install 3.12   # Install Python 3.12
uv python list           # List installed versions
```

#### Set Project Python Version
```bash
uv python pin 3.11       # Pin project to Python 3.11
```

## Running Code

#### Run Python Scripts
```bash
uv run python script.py   # Run with project venv
uv run --python 3.11 script.py  # Run with specific version
```

#### Run Commands in Environment
```bash
uv run pytest            # Run pytest in project env
uv run django-admin startproject mysite
```

## Lock File Management

#### Generate Lock File
```bash
uv lock                  # Generate uv.lock
uv lock --upgrade        # Upgrade all dependencies
```

#### Export Lock File
```bash
uv export > requirements.txt        # Export to requirements.txt
uv export --dev > requirements-dev.txt  # Include dev dependencies
```

## Environment Cleanup

#### Remove Virtual Environment
```bash
rm -rf .venv             # Delete .venv directory
```

#### Clean UV Cache
```bash
uv cache clean           # Clean package cache
uv cache dir             # Show cache directory
```

## Useful Environment Variables

#### Set UV Configuration
```bash
export UV_CACHE_DIR=~/.cache/uv     # Set cache directory
export UV_TOOL_DIR=~/.local/share/uv/tools  # Set tools directory
export UV_PYTHON_INSTALL_DIR=~/.local/share/uv/python  # Python install dir
```

## Quick Project Setup Workflow

#### New Project from Scratch
```bash
mkdir myproject && cd myproject
uv init
uv add requests flask
source .venv/bin/activate
uv run python -c "import requests; print('Setup complete!')"
```

#### Existing Project
```bash
cd existing_project
uv init
uv add package1 package2
uv sync
source .venv/bin/activate
```

## Troubleshooting

#### Common Issues
```bash
# If UV not found after installation
source ~/.bashrc         # or ~/.zshrc

# Check if venv is activated
echo $VIRTUAL_ENV

# Reinstall UV
curl -LsSf https://astral.sh/uv/install.sh | sh

# Reset project environment
rm -rf .venv uv.lock
uv sync
```

#### Debug Commands
```bash
uv --verbose run python script.py    # Verbose output
uv doctor                            # System diagnostics (if available)
```


## Installation

#### Method 1: Official Installer (Recommended)
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

#### Method 2: Homebrew
```bash
brew install uv
```

#### Method 3: pipx
```bash
pipx install uv
```

#### Verify Installation
```bash
uv --version
```

#### Update UV
```bash
uv self update
```
