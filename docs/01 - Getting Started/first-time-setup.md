# Setting Up a Clean Mac for Development

## Tools

1. Download [Homebrew](https://brew.sh)
2. Install `git` with `brew install git`
3. Download [Xcode](https://apps.apple.com/us/app/xcode/id497799835?mt=12)
4. Download [Visual Studio Code](https://code.visualstudio.com)
5. Download [JetBrains Toolbox](https://www.jetbrains.com/toolbox-app/)
6. Download [Fast Node Manager (fnm)](https://github.com/Schniz/fnm)
7. Download latest Node.js with `fnm install --lts`
8. Download [Claude Code](https://www.claude.com/product/claude-code)
9. Download [uv](https://github.com/astral-sh/uv)
10. Download [Java OpenJDK 17](https://formulae.brew.sh/formula/openjdk@17)
11. Download [Deno](https://deno.com/)
12. Download [OrbStack](https://orbstack.dev/)

## Setup git

```bash
git config --global init.defaultBranch master
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

## Setup automatic git signing

1. Generate a new SSH key (or use an existing one):

```bash
ssh-keygen -t ed25519 -C "your.email@example.com"
```

2. Configure git to sign commits and tags with your SSH key:

```bash
git config --global commit.gpgsign true
git config --global gpg.format ssh
git config --global user.signingkey ~/.ssh/path/to/your/key.pub
```
