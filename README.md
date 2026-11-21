# My Kitty Setup

My [kitty](https://sw.kovidgoyal.net/kitty/) settings for Omarchy.

Docs: https://sw.kovidgoyal.net/kitty/conf/

## Setup

Clone this repository to `~/.config/kitty`, so the checkout is the live config.
The [setup](https://github.com/anwarahmed/setup) repo does this on every machine.

Colors come from the current Omarchy theme, through the `include` at the top of
`kitty.conf`. Everything below it overrides Omarchy's defaults in
`/etc/xdg/kitty/kitty.conf`.

Reload running kittys after a change with `omarchy restart terminal`.

The earlier macOS config is kept at the `archive/macos` tag.
