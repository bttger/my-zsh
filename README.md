# Zsh without bloated plugin or theme manager

It may be tempting to quickly install Oh-my-Zsh and Powerlevel10k or other plugin managers. They allow you to configure Zsh in no time without any prior knowledge. But they also bring a lot of bloat with them. Instead, I want to decide for myself what I install on my machine, when I update packages, and be able to follow and customize the configuration process.

![image](https://user-images.githubusercontent.com/49961674/201792373-88dec4d2-7c48-403a-8fc1-a03e9d0f61c1.png)

## Features
- Use your OS package manager and source/configure all plugins in a single file
- Case-insensitive, misspell-forgiving completions
- Emacs keybindings paired with "normal" text editor keybindings (See [Keybindings](#keybindings))
- Convenient aliases (See [Aliases](#aliases))
- [tere](https://github.com/mgunyho/tere) integration for easy and fast directory navigation
- Long history with immediate history udpates and duplicate omission (duplicates move to end of history)
- Commands beginning with space won't be saved in history
- Clean prompt with git status, exit code of last command if code != 0, and optionally displaying hostname
- [Autosuggestions based on history](https://github.com/zsh-users/zsh-autosuggestions)
- Search through history for previous commands matching everything up to current cursor position with arrow keys
- [Syntax highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)
- Autocomplete with [fzf](https://github.com/junegunn/fzf) fuzzy search

## Keybindings
TODO

## Aliases
TODO

## Install

### Arch Linux
```
pacman -Syu TODO
chsh -s $(which zsh)
```
