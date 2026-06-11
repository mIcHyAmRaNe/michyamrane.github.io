---
title: First Steps After Installing Ubuntu
date: 2026-06-11
categories:
  - linux
---

## 1. System Update

```bash
sudo apt update && sudo apt upgrade -y
```

## 2. Install Build Essentials

```bash
sudo apt install build-essential
```

This installs `gcc`, `g++`, `make`, and other tools needed for compiling software.

<!-- more -->

## 3. Python is Python3 & UV

Ubuntu ships with Python 3 but `python` points to `python3` only after installing this package.

```bash
sudo apt install python-is-python3 python3-pip
```

Install [uv](https://docs.astral.sh/uv/) — a fast Python package and project manager (replaces pip, venv, pip-tools, poetry):

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

## 4. Install Zsh & Set as Default Shell

```bash
sudo apt install zsh
chsh -s $(which zsh)
```

Log out and back in (or reboot) for the change to take effect.

## 5. Install Starship Prompt

```bash
curl -sS https://starship.rs/install.sh | sh
```

Add this to the end of `~/.zshrc`:

```bash
eval "$(starship init zsh)"
```

## 6. Starship Configuration

Create `~/.config/starship.toml`:

```toml
# Inserts a blank line between shell prompts
add_newline = true

format = """
[┌╴](bold green)[$username㉿$hostname](bold blue)[\]](bold green)$os$time \
| $all[└─](green) $character\
"""

[character]
success_symbol = "💲"
error_symbol = "✗"

[username]
style_user = 'blue bold'
style_root = 'red bold'
format = '[$user]($style)'
disabled = false
show_always = true

[hostname]
ssh_only = false
format = '[$ssh_symbol](bold blue)[$hostname](bold blue)'
trim_at = '.companyname.com'
disabled = false

[os]
style = "bold green"
format = "on [$symbol$arch$name](style)"
disabled = false

[os.symbols]
Windows = "💠"
Linux = "🐧"
```

## 7. Git & SSH Setup

```bash
sudo apt install git
```

Then follow my post on [SSH Keys for Git Authentication](./git_auth_ssh.md).
