# CLAUDE.md

Guidance for Claude Code in this repository.

## What this repo is

The [kitty](https://sw.kovidgoyal.net/kitty/conf/) configuration for **two machines**, checked
out **directly into `~/.config/kitty`** on each, so the repo root is the live config directory:

- **Omarchy** (Linux). The [setup repo](https://github.com/anwarahmed/setup) clones it there.
- **The work laptop** (macOS), still in daily use.

Both pull `main`. A change for one machine must not change the other.

## Layout

`kitty.conf` holds only settings every machine should have, then `include ${KITTY_OS}.conf`.
kitty sets `KITTY_OS` to `linux`, `macos` or `bsd`, and relative includes resolve next to the
including file. So:

- `linux.conf`: the Omarchy config.
- `macos.conf` plus `current-theme.conf` (the grape theme): the work laptop's config. Its
  settings are exactly the ones the old single-file macOS config had; the archived original is
  at the `archive/macos` tag (the full commented default file, `07ad0e1`).

Put a setting in `kitty.conf` only when both machines should get it, and say so in the PR. When
unsure, put it in the OS file. There's no kitty on the Omarchy dev machine to test with, so check
a change by expanding the includes for each OS and diffing the active lines against `main`.

## linux.conf (Omarchy)

1. `/etc/xdg/kitty/kitty.conf`: Omarchy's defaults, owned by the `omarchy-settings` package.
2. `include ~/.local/state/omarchy/current/theme/kitty.conf`: the current Omarchy theme's colors.
   Keep this line first in `linux.conf`, or kitty stops following `omarchy theme set`. With
   glassy windows on, Omarchy also writes a see-through background into that theme file, so no
   opacity or blur settings belong in `linux.conf`.
3. Everything else in `linux.conf` overrides the two above.

- The `send_text` maps for Shift+Enter (`\e[13;2u`) and Alt+Shift+Enter (`\e[13;4u`) send CSI-u
  so TUIs and tmux can tell them from plain Enter. tmux binds `M-S-Enter`; don't drop the second.
- `listen_on unix:${XDG_RUNTIME_DIR}/omarchy-kitty-{kitty_pid}` was added by Omarchy migration
  `1784479832.sh`. Omarchy's "new terminal in the current directory" keybinding uses it.
- `allow_remote_control yes` is commented out on purpose: Omarchy migration `1788745941.sh`
  disables unrestricted remote control as a security fix.
- Copy and paste use Ctrl+Insert and Shift+Insert, matching the foot config.

**Omarchy migrations edit `~/.config/kitty/kitty.conf` by name**, not `linux.conf`. If one
appends a line (as `1784479832.sh` did with `listen_on`), it lands in the shared file and would
reach the Mac: move it into `linux.conf`. They also leave `kitty.conf.bak.XXXXXX` backups, which
are gitignored; delete them.

## Working in this repo

Changes land through pull requests to `main` (a "Main" ruleset requires them), squash merged.
