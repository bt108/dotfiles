# Dotfiles

[![license MIT](https://img.shields.io/badge/license-MIT-green)](LICENSE)

Personal dotfiles for a NixOS daily driver. [Neovim](https://neovim.io)
(lazy.nvim, fzf-lua, oil, leap), [fish](https://fishshell.com) with vi
keybindings, [kitty](https://sw.kovidgoyal.net/kitty/) with auto light/dark
themes, a [NixOS](https://nixos.org) system configuration, and small CLI
tooling — laid out as a `$HOME` overlay you copy into place.

## 30-second example

```sh
git clone https://github.com/bt108/dotfiles.git ~/dotfiles
cp -r ~/dotfiles/.config ~/dotfiles/.local ~/
cp ~/dotfiles/.gitconfig ~/
```

Keep the machine awake while a long command runs:

```sh
~/.local/bin/keepalive echo hello
# Acquiring inhibitor and running: echo hello
# hello
```

## Contents

| Path | What it is |
|---|---|
| `.config/nvim/` | Neovim (lazy.nvim, self-bootstrapping): `init.lua` + `lua/` (plugins, options, keymaps, helpers) — `<leader>y/p` clipboard, `gj/gk` movement, `<C-j>/<C-k>` paging, fzf-lua/oil/grug-far bindings, `<++>` fill |
| `.config/fish/config.fish` | fish: adds `~/.local/bin` to `PATH`, `rmi` alias, vi keybindings |
| `.config/kitty/` | `kitty.conf` (F1–F5 tab/window shortcuts) plus auto `dark`/`light`/`no-preference` themes |
| `.config/nixos/configuration.nix` | NixOS config: GNOME, fish/neovim, abbreviations (`nv`, `yt-*`, `cnx*`), packages, fonts, vnstat |
| `.config/fd/ignore` | Ignore rules for `fd` |
| `.local/bin/keepalive` | `keepalive COMMAND [ARGS…]` — runs the command under `systemd-inhibit --what=idle:sleep` so downloads/players don't get suspended |
| `.gitconfig` | Git aliases (`s`, `co`, `lo`, `logPretty`, …), `delta` pager, `zdiff3` merge style |
| `.claude/` | Claude Code `settings.json` plus a gruvbox `statusline-command.sh` (repo/branch, diff velocity, context usage, model) |

## Install

Prerequisites: `git`, plus whichever tools you use — `nvim`, `fish`,
`kitty`, `fd`, [`delta`](https://github.com/dandavison/delta) (git pager).
Neovim plugins install themselves on first launch via lazy.nvim.

```sh
git clone https://github.com/bt108/dotfiles.git ~/dotfiles
cp -r ~/dotfiles/.config ~/dotfiles/.local ~/
cp ~/dotfiles/.gitconfig ~/
```

## Machine notes

- Everything except `.config/nixos/configuration.nix` is portable Linux;
  that file is NixOS-only (`sudo nixos-rebuild switch`).
- Machine-specific: hostname `nixos`, user `taraka`, timezone
  `Asia/Kolkata`, imports `/etc/nixos/hardware-configuration.nix` —
  adjust before reuse.
- `.claude/settings.json` hardcodes the statusline path as
  `/home/taraka/.claude/statusline-command.sh`; update it if your username differs.

## License

MIT — see [LICENSE](LICENSE).
