# Mac OS X Local Development Environment Setup

## Tools

- git
- [Homebrew](https://brew.sh)
- [pyenv](https://github.com/pyenv/pyenv)
- [nvm](https://github.com/nvm-sh/nvm)
- [pipx](https://github.com/pypa/pipx)
- [Poetry](https://python-poetry.org/docs/#installation)
- [Pipenv](https://github.com/pypa/pipenv)

## Installing Xcode CLI Tools

```bash
xcode-select --install
```

## Installing Homebrew

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

> source: https://brew.sh

## Install Helpful CLI Tools

```bash
brew install jq watchman gnupg
```

## Setup Git

### Install Git from Homebrew

```bash
brew install git
```

### Installing Git Credential Manager (CFA)

```bash
brew tap microsoft/git
```

```bash
brew install --cask git-credential-manager
```

```bash
git config --global user.name "Jalo Moster"
```

```bash
git config --global user.email "jlvmoster@gmail.com"
```

```bash
git config --global init.defaultBranch master
```

## Installing Node w/ nvm

Install/update nvm

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.2/install.sh | bash
```

> source: https://github.com/nvm-sh/nvm?tab=readme-ov-file#install--update-script

Install latest Node version

```bash
nvm install --lts
```

## Installing Python w/ pyenv

### Prerequisites

```bash
brew install openssl readline sqlite3 xz zlib tcl-tk@8 libb2
```

### Install Pyenv and Python

```bash
brew install pyenv
```

> source: https://github.com/pyenv/pyenv?tab=readme-ov-file#d-install-python-build-dependencies

Install latest Python version

```bash
pyenv install 3
```

Set default Python version

```bash
pyenv global 3
```

## Installing Poetry

Install pipx

```bash
brew install pipx
pipx ensurepath
sudo pipx ensurepath --global # optional to allow pipx actions with --global argument
```

> source: https://github.com/pypa/pipx?tab=readme-ov-file#on-macos

Install Poetry

```bash
pipx install poetry
```

### Setup autocomplete (recommended)

Create the `.zfunc` directory

```bash
mkdir .zfunc
```

Generate the poetry auto completion script

```bash
poetry completions zsh > ~/.zfunc/_poetry
```

Add to the `.zshrc` file

```bash
fpath+=~/.zfunc
autoload -Uz compinit && compinit
```

### Recommended Configuration

To enable poetry to create and utilize the `.venv` virtual environment directory inside the project root folder, run the following command:

```bash
poetry config virtualenvs.in-project true
```

> source: https://python-poetry.org/docs/configuration/#virtualenvsin-project

## Installing Pipenv

Install Pipenv

```bash
pipx install pipenv
```

### Setup autocomplete (recommended)

Modify `.zshrc` to include after the line `export PATH="$PATH:/Users/jalo.moster/.local/bin"`:

```bash
# Setup Pipenv autocomplete
eval "$(_PIPENV_COMPLETE=zsh_source pipenv)"
```

### Recommended Configuration

To enable pipenv to create and utilize the `.venv` virtual environment directory inside the project root folder, add the following environment variable to the `.zshenv` file:

```bash
# Set Pipenv global configurations
export PIPENV_VENV_IN_PROJECT=1
```
