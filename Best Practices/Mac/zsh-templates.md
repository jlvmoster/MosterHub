## .zprofile

```bash
###########################################################
# This file is reserved for login-specific configurations #
###########################################################

# Setup Homebrew
eval "$(/opt/homebrew/bin/brew shellenv)"

# Added by OrbStack: command-line tools and integration
# This won't be added again if you remove it.
source ~/.orbstack/shell/init.zsh 2>/dev/null || :

```

## .zshenv

```bash
##########################################################
# This file is reserved for global environment variables #
##########################################################

# Specify Java version
export JAVA_HOME=$(/usr/libexec/java_home -v 17)

```

## .zshrc

```bash
########################################################
# This file is reserved for interactive shell behavior #
########################################################

# Setup .zfunc directory and additional completions here
fpath=(/Users/[YOUR_USERNAME]/.zfunc /opt/homebrew/share/zsh/site-functions $fpath)
autoload -Uz compinit && compinit

# Setup 1Password environment variables
export EXAMPLE_1PASSWORD_SECRET=$(op read "op://Personal/43qnzaovikkbyaahclokeoq6ya/master-password")

# fnm
FNM_PATH="/opt/homebrew/opt/fnm/bin"
if [ -d "$FNM_PATH" ]; then
  eval "`fnm env`"
fi

# Setup fnm shell environment
eval "$(fnm env --use-on-cd --shell zsh)"

# Setup local binaries
export PATH="$PATH:/Users/[YOUR_USERNAME]/.local/bin"

# Added by Toolbox App
export PATH="$PATH:/Users/[YOUR_USERNAME]/Library/Application Support/JetBrains/Toolbox/scripts"

# Setup OpenJDK 17
export PATH="/opt/homebrew/opt/openjdk@17/bin:$PATH"

# Setup local Claude Code
alias claude="/Users/[YOUR_USERNAME]/.claude/local/claude"

. "$HOME/.local/bin/env"

# Setup uv and uvx shell auto completions
eval "$(uv generate-shell-completion zsh)"
eval "$(uvx --generate-shell-completion zsh)"

# Setup Deno
. "/Users/jalo/.deno/env"

```

## Appendix

### Setup fnm autocompletion

```bash
mkdir -p ~/.zfunc && fnm completions --shell zsh >> .zfunc/fnm
```

### Migrate Claude Code to local installation

```bash
claude migrate-installer
```
