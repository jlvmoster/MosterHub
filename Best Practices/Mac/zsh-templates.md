## .zprofile

```bash
###########################################################
# This file is reserved for login-specific configurations #
###########################################################

# Setup Homebrew
eval "$(/opt/homebrew/bin/brew shellenv)"

```

## .zshenv

```bash
##########################################################
# This file is reserved for global environment variables #
##########################################################

# Setup Pyenv root
export PYENV_ROOT="$HOME/.pyenv"

# Setup NVM dir
export NVM_DIR="$HOME/.nvm"

# Specify Java version
export JAVA_HOME=$(/usr/libexec/java_home -v 1.8)

# Setup Poetry environment variables
export POETRY_EXAMPLE="This is an example environment available in Poetry environments"

# Set Pipenv global configurations
export PIPENV_VENV_IN_PROJECT=1

```

## .zshrc

```bash
########################################################
# This file is reserved for interactive shell behavior #
########################################################

# Setup .zfunc directory
fpath+=~/.zfunc
autoload -Uz compinit && compinit

# Setup Pyenv
[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"

# Setup 1Password environment variables
export EXAMPLE_1PASSWORD_SECRET=$(op read "op://Personal/43qnzaovikkbyaahclokeoq6ya/master-password")

# Setup NVM
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion" # This loads nvm bash_completion

# Setup Databricks CLI completion
fpath+=/opt/homebrew/share/zsh/site-functions
autoload -Uz compinit && compinit

# Setup local binaries
export PATH="$PATH:/Users/[YOUR_USERNAME]/.local/bin"

# Setup Pipenv autocomplete
eval "$(_PIPENV_COMPLETE=zsh_source pipenv)"

# Added by Toolbox App
export PATH="$PATH:/Users/[YOUR_USERNAME]/Library/Application Support/JetBrains/Toolbox/scripts"

```
