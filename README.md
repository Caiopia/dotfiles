# dotfiles

A small macOS setup repo for shell config, Git, terminal preferences, and the
base packages I want on a clean machine.

## What this repo does

- Installs Homebrew and the CLI tools declared in [Brewfile](Brewfile)
- Links repo-managed config into the home directory
- Sets up zsh + Starship for the terminal experience plus a few modern tools.
- Configures git identity using `gh` and ignore rules
- Applies some macOS defaults I prefer on install
- Re-runs cleanly and safely on top of an existing machine

## Install

Obviously you can just clone this, but for a cheeky one liner:

```bash
curl -fsSL https://raw.githubusercontent.com/Caiopia/dotfiles/main/install | bash
```

Then, from the repo later if making changes:

```bash
./install
```

The one liner installs the repo under `~/Developer` by default; you get a nice macOS hammer icon by default in Finder. Set `DEV_HOME` first if you want it elsewhere.

## What gets set up

| Area | Repo file | Installed location | Purpose |
| --- | --- | --- | --- |
| Shell config | [config/zshrc](config/zshrc) | `~/.zshrc` | Main zsh setup |
| Prompt | [config/starship.toml](config/starship.toml) | `~/.config/starship.toml` | Terminal prompt styling |
| Terminal app | [config/ghostty/config](config/ghostty/config) | `~/.config/ghostty/config` | Ghostty settings |
| Git config | [config/git/config](config/git/config) | `~/.gitconfig` | Git defaults |
| Git ignores | [config/git/ignore](config/git/ignore) | `~/.config/git/ignore` | Shared ignore rules |
| Packages | [Brewfile](Brewfile) | system package manager | CLI tools and packages |
| macOS defaults | [macos.defaults](macos.defaults) | system settings | Standard defaults |

## Where to find things

- Repo root: [dotfiles](.)
- Shell config: [config](config)
- Git config: [config/git](config/git)
- Install script: [install](install)
- Package list: [Brewfile](Brewfile)
- macOS defaults: [macos.defaults](macos.defaults)

## Notes

- These are symlinks, not copies, so changes in the repo take effect immediately.
- Existing target files are backed up instead of overwritten.
- Machine-local shell tweaks can go in `~/.zshrc.local` and are sourced automatically.
- Git identity is not stored in the repo; it lives in `~/.config/git/identity` and is created from `GIT_NAME` / `GIT_EMAIL` or from the signed-in GitHub account when available.
