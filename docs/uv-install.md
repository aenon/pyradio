# Installing PyRadio with uv

This fork is designed to be installed with [uv](https://docs.astral.sh/uv/), specifically via `uv tool` which provides isolated, user-wide command-line tools.

## Prerequisites

- Python 3.12+
- [uv](https://docs.astral.sh/uv/) installed (`curl -LsSf https://astral.sh/uv/install.sh | sh`)
- MPV, MPlayer, or VLC installed and in your `$PATH`

## Install

### From GitHub (recommended)

```bash
uv tool install git+https://github.com/aenon/pyradio.git
```

### From a local clone

```bash
git clone git@github.com:aenon/pyradio.git
uv tool install ./pyradio
```

This installs `pyradio` and `pyradio-client` into `~/.local/bin/` (ensure this is on your `$PATH`).

## Update

After pulling new changes (or to force a reinstall):

```bash
uv tool install ./pyradio --force
```

Or reinstall directly from remote:

```bash
uv tool install git+https://github.com/aenon/pyradio.git --force
```

## Uninstall

```bash
uv tool uninstall pyradio
```

## Syncing with upstream

This fork tracks [coderholic/pyradio](https://github.com/coderholic/pyradio). To pull upstream updates:

```bash
# One-time: add upstream remote
git remote add upstream git@github.com:coderholic/pyradio.git

# Fetch and merge upstream into your master
git fetch upstream
git checkout master
git merge upstream/master
git push origin master

# Reinstall after update
uv tool install . --force
```

If you have local commits on master and prefer a clean history:

```bash
git fetch upstream
git rebase upstream/master
git push --force-with-lease origin master
uv tool install . --force
```

## How it works

`uv tool install` creates an isolated virtualenv at `~/.local/share/uv/tools/pyradio/` with all Python dependencies, then symlinks the console scripts (`pyradio`, `pyradio-client`) into `~/.local/bin/`. This keeps your system Python clean while making the commands globally available to your user.

## Troubleshooting

**`pyradio: command not found`** — Ensure `~/.local/bin` is on your `$PATH`. Add to your shell rc:

```bash
export PATH="$HOME/.local/bin:$PATH"
```

**Player not found** — `mpv`, `mplayer`, or `vlc` must be installed as system packages (e.g., `brew install mpv` on macOS).
