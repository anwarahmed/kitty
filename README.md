# My Kitty Setup

My [kitty](https://sw.kovidgoyal.net/kitty/) settings, for Omarchy and macOS.

Docs: https://sw.kovidgoyal.net/kitty/conf/

## Layout

| File | Used on | Holds |
|---|---|---|
| `kitty.conf` | every machine | settings shared by all, then `include ${KITTY_OS}.conf` |
| `linux.conf` | Omarchy | Omarchy theme colors, JetBrainsMono 9pt, tab bar, keys |
| `macos.conf` | macOS (work laptop) | MesloLGS 12pt, opacity and blur, `macos_*` settings |
| `current-theme.conf` | macOS | the grape color theme |

kitty sets `KITTY_OS` to `linux`, `macos` or `bsd` itself, so each machine
picks up its own file with no setup.

## Setup

Clone this repository to `~/.config/kitty`, so the checkout is the live config.
On Omarchy the [setup](https://github.com/anwarahmed/setup) repo does this.

Reload after a change: `omarchy restart terminal` on Omarchy, or
<kbd>ctrl</kbd>+<kbd>cmd</kbd>+<kbd>,</kbd> on macOS.
