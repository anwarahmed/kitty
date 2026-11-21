# CLAUDE.md

Guidance for Claude Code in this repository.

## What this repo is

A single-file [kitty](https://sw.kovidgoyal.net/kitty/conf/) configuration (`kitty.conf`)
checked out **directly into `~/.config/kitty`** on Omarchy. The repo root *is* the live config
directory, so editing `kitty.conf` here edits the running config. The
[setup repo](https://github.com/anwarahmed/setup) clones it there (its `DOTFILES` table).

The macOS config this repo used to hold (MesloLGS, a grape theme, `macos_*` settings) is at the
`archive/macos` tag. It is not coming back to `main`.

## How the config is layered

1. `/etc/xdg/kitty/kitty.conf`: Omarchy's defaults, owned by the `omarchy-settings` package.
2. `include ~/.local/state/omarchy/current/theme/kitty.conf`: the current Omarchy theme's colors.
   Keep this line first, or kitty stops following `omarchy theme set`. With glassy windows on,
   Omarchy also writes a see-through background into that theme file, so no opacity or blur
   settings belong here.
3. Everything else in `kitty.conf` overrides the two above.

Apply changes with `omarchy restart terminal`. `allow_remote_control` and `listen_on` are read
only at startup, so changing them needs a new kitty window.

## Settings that matter

- The `send_text` maps for Shift+Enter (`\e[13;2u`) and Alt+Shift+Enter (`\e[13;4u`) send CSI-u
  so TUIs and tmux can tell them from plain Enter. tmux binds `M-S-Enter`; don't drop the second.
- `listen_on unix:${XDG_RUNTIME_DIR}/omarchy-kitty-{kitty_pid}` was added by Omarchy migration
  `1784479832.sh`. Omarchy's "new terminal in the current directory" keybinding uses it.
- `allow_remote_control yes` is commented out on purpose: Omarchy migration `1788745941.sh`
  disables unrestricted remote control as a security fix and leaves a `kitty.conf.bak.XXXXXX`
  beside the file. Those backups are gitignored; delete them.
- Copy and paste use Ctrl+Insert and Shift+Insert, matching the foot config.

## Working in this repo

Changes land through pull requests to `main` (a "Main" ruleset requires them), squash merged.
