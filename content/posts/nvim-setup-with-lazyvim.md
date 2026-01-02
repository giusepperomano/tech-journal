---
Title: Neovim Setup with LazyVim
date: 2024-12-31
tags:
- computing
- linux
---
## Introduction

LazyVim is a preconfigured Neovim setup built on top of the
[lazy.nvim](https://github.com/folke/lazy.nvim) plugin manager. It provides a
sensible default configuration while still allowing full customization.

## Install Neovim

LazyVim requires Neovim 0.9.0 or later. On Ubuntu 22.04, the repository
version is older, so install it via snap:

```bash
linux:~> sudo snap install nvim
```

Verify the installed version with the following command:

```bash
linux:~> nvim --version
```

## Install LazyVim

Install the prerequisite packages:

```bash
linux:~> sudo apt-get install fzf
```

If you already have Neovim configuration, back it up:

```bash
linux:~> mv ~/.config/nvim ~/.config/nvim.bak
linux:~> mv ~/.local/share/nvim ~/.local/share/nvim.bak
```

Clone the LazyVim starter repository:

```bash
linux:~> git clone https://github.com/LazyVim/starter ~/.config/nvim
linux:~> cd  ~/.config/nvim
linux:~> rm -rf .git
```

(removing the '.git' directory lets you manage the configuration as your own
project).

Start Neovim:

```bash
linux:~> nvim
```

The lazy.nvim plugin manager will automatically download and install plugins
the first time it starts. Restart Neovim once the installation completes. 

## Install NerdFonts

Some Neovim plugins require a Nerd Font for icons. Download and extract the font
files from the Nerd Font website (for example Cascadia Mono):

```bash
linux:~> mkdir -p $HOME/.fonts/NerdFonts && cd $HOME/.fonts/NerdFonts
linux:~> wget https://github.com/ryanoasis/nerd-fonts/releases/download/v3.4.0/CascadiaMono.zip
linux:~> unzip CascadiaMono.zip
linux:~> rm -f CascadiaMono.zip
```

Update the font cache:

```bash
linux:~> fc-cache -fv
```

Select the font in your GNOME Terminal profile (GNOME Teminal &rarr; Preferences
&rarr; [Profile Name] &rarr; Text):

## Further Customization

Neovim stores user configuration in the '~/.config/nvim/lua' directory. You can add
or override options by editing 'lua/config/options.lua' (create it if it doesn't
exist):

```lua
-- Force dark background:
vim.go.background = "dark"

-- Disable relative line numbers:
set vim.opt.relativenumber = false

-- Show all characters in Markdown files:
vim.opt.conceallevel = 0
```

After editing, restart Neovim.

## Links

- [Effective Neovim setup for web development towards 2024](https://www.devas.life/effective-neovim-setup-for-web-development-towards-2024/)
- [Sample init.lua](https://github.com/jonhoo/configs/blob/master/editor/.config/nvim/init.lua)
- [LazyVim issue (default background color)](https://github.com/LazyVim/LazyVim/issues/279)
- [Sample init.lua](https://github.com/craftzdog/dotfiles-public/blob/master/.config/nvim/init.lua)
- [NeoVim hides the * chars when editing markdown](https://vi.stackexchange.com/questions/6512/neovim-hides-the-chars-when-editing-markdown)
- [Nerd Fonts Downloads](https://www.nerdfonts.com/font-downloads)
- [Neovim Configuration for Beginners](https://builtin.com/software-engineering-perspectives/neovim-configuration)
