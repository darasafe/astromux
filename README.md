# astromux

My tmux setup — and the terminal stack it flies with. Catppuccin Macchiato, a clean
Nerd Font status bar, vi copy-mode, and a small set of pinned plugins. Copy one file,
start tmux, press one key.

## Install

```sh
git clone https://github.com/darasafe/astromux.git
cp astromux/.tmux.conf ~/.tmux.conf      # or symlink: ln -s "$PWD/astromux/.tmux.conf" ~/.tmux.conf
tmux                                      # first start auto-installs TPM + plugins
```

Inside tmux: `prefix + I` installs plugins, `prefix + r` reloads. **prefix is `Ctrl-b`**
(tmux default). If the bar looks unstyled, you're missing the Nerd Font — see below.

## Match my exact look

The bar theme (**Catppuccin Macchiato**) ships in the config; the rest is terminal-side. To mirror mine:

- **Terminal:** Windows Terminal.
- **Font: Hack Nerd Font** — install it from [nerdfonts.com](https://www.nerdfonts.com/font-downloads),
  then *Settings → your WSL/Ubuntu profile → Appearance → Font face → `Hack Nerd Font`*. Without a
  Nerd Font the status glyphs (clock, calendar, wifi, battery) render as empty boxes.
- **Background:** set the profile background to `#171421` (*Appearance → Background*).
- **tmux ≥ 3.x** required (catppuccin v2, `absolute-centre`). Check with `tmux -V`.

## Keys worth knowing

| Action | Keys |
| --- | --- |
| Reload config | `prefix` `r` |
| Move between panes | `prefix` `h/j/k/l` |
| Resize panes | `Alt-h/j/k/l` |
| Copy mode (scrollback) | `prefix` `[` → `v` select, `y` yank, `q` quit |
| File-picker popup | `prefix` `Ctrl-f` |
| Install plugins | `prefix` `I` |

`Alt`-resize needs the Neovim half (`smart-splits.nvim`) for seamless nvim↔tmux nav; `prefix+Ctrl-f`
needs a `tmux-file-picker` binary on `PATH`. Both no-op if absent.

## The wider setup it pairs with

The tmux config stands alone, but it's one piece of a Catppuccin-Macchiato terminal. Optional companions:

| Tool | Role |
| --- | --- |
| **Catppuccin Macchiato** | one theme across tmux, lazygit/delta, bat |
| **Starship** | cross-shell prompt (zsh) |
| **eza · bat · fd · ripgrep** | modern `ls` / `cat` / `find` / `grep` |
| **fzf · zoxide** | fuzzy finder + smart `cd` |
| **lazygit + delta** | git TUI with themed diffs |
| **tmux-resurrect + continuum** | save/restore sessions across reboots |
| **chezmoi** | manages all of it as dotfiles |

## Plugins (pinned)

Pinned to upstream tags for reproducible installs (tags are mutable — reproducible, not
commit-immutable): tpm · catppuccin/tmux · tmux-battery · tmux-online-status ·
tmux-resurrect · tmux-continuum · smart-splits.nvim.

## Notes

- **First launch downloads and runs third-party plugin code** from GitHub (standard TPM) — skim the list above first if that matters to you.
- **Session auto-restore is on** (`@continuum-restore`); comment it out in `~/.tmux.conf` to start fresh each time.
- Resurrect state under `~/.tmux/resurrect/` can hold working dirs and command history — gitignored here; never commit it publicly.

## License

[MIT](LICENSE).
