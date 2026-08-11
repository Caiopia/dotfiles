# dotfiles

Terminal and shell configuration for macOS — zsh, starship, git, and a small set
of CLI tools. No casks, no language runtimes, no machine-specific assumptions, so
it installs cleanly on a managed or restricted machine.

## Install

```bash
curl -fsSL https://raw.githubusercontent.com/Caiopia/dotfiles/main/bootstrap | bash
```

That clones the repo to `~/Developer/dotfiles`, installs Homebrew if missing, and
runs `./install`. To re-run later, from the repo:

```bash
./install                  # symlinks + brew bundle + macOS defaults
./install --no-packages    # skip brew (also skipped automatically if brew is absent)
./install --no-defaults    # skip macOS defaults
```

Everything happens by default and every step is idempotent — re-running is how
you check the machine is in the right state.

## What gets linked

| Repo file | Target |
|---|---|
| `config/zshrc` | `~/.zshrc` |
| `config/starship.toml` | `~/.config/starship.toml` |
| `config/ghostty/config` | `~/.config/ghostty/config` |
| `config/zellij/config.kdl` | `~/.config/zellij/config.kdl` |
| `config/git/config` | `~/.gitconfig` |
| `config/git/ignore` | `~/.config/git/ignore` |

Symlinks, not copies — edits in `config/` take effect immediately. An existing
file at a target is backed up to `<target>.backup.<timestamp>` rather than
overwritten.

Configs are linked even when the corresponding app isn't installed; the orphan
costs nothing and a later install picks it up.

`~/.gitconfig` rather than `~/.config/git/config`, because git ignores the XDG
path when `~/.gitconfig` exists. Your name and email are *not* in this repo —
they're read from `~/.config/git/identity`, which is untracked:

```ini
[user]
    name = Your Name
    email = you@example.com
```

## Commands

```
dots apply [flags]   re-run ./install
dots push [msg]      commit + push changes
dots edit            open the repo in $EDITOR
```

## Packages

See [`Brewfile`](Brewfile). Both `zellij` and `herdr` are installed for now —
they're competing multiplexers and one will eventually be dropped.

## macOS defaults

[`macos.defaults`](macos.defaults) is applied on every install. Keys locked by
MDM are reported and skipped; the rest still apply. Personal-taste settings
(Dock, trackpad) deliberately aren't here.
