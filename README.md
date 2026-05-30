# tmux config

An opinionated, beginner-friendly tmux setup: Catppuccin (Macchiato) theme, a clean
status bar, vi-style copy mode, and a small curated set of plugins. Copy it, start tmux,
press one key to install plugins, done.

## Prerequisites

- **tmux ≥ 3.x** — the theme and status-bar format math (`absolute-centre`,
  `#{e|>=:...}`) need a modern tmux. Check with `tmux -V`.
- **git** — used to fetch the plugin manager and plugins.
- **A Nerd Font, set as your terminal font.** The status bar uses icon glyphs
  (clock, calendar, wifi, battery). Without a patched Nerd Font they render as empty
  boxes (“tofu”). Grab one from <https://www.nerdfonts.com/> and select it in your
  terminal settings.

## Install

```sh
git clone https://github.com/darasafe/tmux-config.git
cp tmux-config/.tmux.conf ~/.tmux.conf      # or symlink: ln -s "$PWD/tmux-config/.tmux.conf" ~/.tmux.conf
tmux                                         # start tmux
```

On first start, the config bootstraps [TPM](https://github.com/tmux-plugins/tpm)
(the Tmux Plugin Manager) and installs the plugins automatically. If the bar still
looks unstyled, install/reload plugins manually and reload the config:

1. Press **`prefix` then `I`** (capital i) to install plugins.
2. Press **`prefix` then `r`** to reload the config (or just restart tmux).

> **`prefix` is `Ctrl-b`** in this config (tmux's default — it is not remapped).
> So "`prefix + I`" means: press `Ctrl-b`, release, then press `Shift-i`.

## Key bindings worth knowing (first-timer cheat-sheet)

| Action | Keys |
| --- | --- |
| Reload this config | `prefix` `r` |
| Move between panes | `prefix` `h` / `j` / `k` / `l` |
| Enter scrollback / copy mode | `prefix` `[` (then `q` to quit) |
| Start selection / select line / yank | `v` / `V` / `y` (in copy mode) |
| Resize panes | `Alt-h/j/k/l` (smart-splits) |
| Open file picker popup | `prefix` `Ctrl-f` |
| Scroll up into copy mode | `PageUp` |

Everything else (new window `prefix c`, split is via panes, detach `prefix d`, etc.)
is stock tmux — the [tmux man page](https://man7.org/linux/man-pages/man1/tmux.1.html)
or any "tmux cheat sheet" covers the basics.

## Plugins (pinned)

Versions are pinned to upstream tags for reproducible installs. Bump them deliberately.

- `tmux-plugins/tpm` — plugin manager
- `catppuccin/tmux` — theme
- `tmux-plugins/tmux-battery`, `tmux-online-status` — status-bar widgets
- `tmux-plugins/tmux-resurrect`, `tmux-continuum` — save/restore sessions

Two bindings depend on extra tooling and simply do nothing if it is absent:

- **`Alt-h/j/k/l` resize** is provided by the tmux side of
  `mrjones2014/smart-splits.nvim`; the seamless nvim↔tmux navigation half only
  matters if you use Neovim with that plugin.
- **`prefix + Ctrl-f`** needs a `tmux-file-picker` binary on your `PATH`.

## Notes

- **First launch downloads and runs third-party code.** On first start the config
  clones TPM and the pinned plugins from GitHub and executes them inside tmux. Versions
  are pinned to upstream tags; tags are mutable, so this is reproducible but not
  commit-immutable. Skim the plugin list above before installing if that matters to you.
- **Session auto-restore is on** (`@continuum-restore 'on'`): tmux tries to restore a
  previous session on launch. Comment that line out in `~/.tmux.conf` if you'd rather
  start fresh each time.
- Resurrect/continuum save state under `~/.tmux/resurrect/`. That state can contain
  your working directories and command history — it is gitignored here and should
  never be committed anywhere public.
