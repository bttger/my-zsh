# Zsh without bloated plugin or theme manager

It may be tempting to quickly install Oh-my-Zsh and Powerlevel10k or other plugin managers. They allow you to configure Zsh in no time without any prior knowledge. But they also bring bloat with them. Instead, I want to decide for myself what I install on my machine, when I update packages, and be able to follow and customize my configuration.

![image](https://user-images.githubusercontent.com/49961674/201792373-88dec4d2-7c48-403a-8fc1-a03e9d0f61c1.png)

## Features
- Use your OS package manager and source/configure all plugins in a single file
- Case-insensitive, misspell-forgiving completions
- Emacs keybindings paired with common text editor keybindings (See [Keybindings](#keybindings))
- Convenient aliases (See [Aliases](#aliases))
- [tere](https://github.com/mgunyho/tere) integration for easy and fast directory navigation
- Long history with immediate history updates and duplicate omission (duplicates move to end of history)
- Commands beginning with space won't be saved in history
- Clean prompt with git status, exit code of last command if code != 0, and optionally displaying hostname
- [Autosuggestions](https://github.com/zsh-users/zsh-autosuggestions) based on history
- Search through history for previous commands matching everything up to current cursor position with arrow keys
- [Syntax highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)
- Autocomplete and history search with [fzf](https://github.com/junegunn/fzf) fuzzy search

## Keybindings
The default config enables Emacs keybindings but you can disable them or change them to vi by swapping out the `-e` flag with `-v` in [line 17](https://github.com/bttger/my-zsh/blob/main/.zshrc#L17). The following keybindings add features known from common text editors:

- <kbd>Home</kbd> to move cursor to the beginning of the line
- <kbd>End</kbd> to move cursor to the end of the line
- <kbd>Del</kbd> to delete the following char
- <kbd>Ctrl</kbd> + <kbd>Del</kbd> to delete the following word
- <kbd>Ctrl</kbd> + <kbd>⌫</kbd> to delete the previous word
- <kbd>Ctrl</kbd> + <kbd>→</kbd> to move cursor forward one word
- <kbd>Ctrl</kbd> + <kbd>←</kbd> to move cursor backward one word
- <kbd>Ctrl</kbd> + <kbd>Z</kbd> to undo last action
- <kbd>Ctrl</kbd> + <kbd>Y</kbd> to redo undone actions

Autosuggestions:
- <kbd>Ctrl</kbd> + <kbd>→</kbd> to partially accept suggestion up to the point that the cursor moves to
- <kbd>End</kbd> or <kbd>→</kbd> to accept suggestion and replace contents of the command line buffer with the suggestion

Fuzzy search:
- <kbd>Ctrl</kbd> + <kbd>T</kbd> to fuzzy search files/directories and paste the selected files/directories onto the command line
- <kbd>Ctrl</kbd> + <kbd>R</kbd> to fuzzy search the history and paste the selected command onto the command line
- <kbd>Alt</kbd> + <kbd>C</kbd> to fuzzy search directories and `cd` into the selected directory
- Type `**` and hit <kbd>Tab</kbd> to fuzzy search files/directories/process IDs/hostnames/environment variables, and autocomplete command

History search:
- Type beginning of some command and use <kbd>↑</kbd> and <kbd>↓</kbd> to search through the history for previous commands matching everything up to current cursor position

## Aliases
| alias     | command             |
|--------|----------------------|
|`md`|`mkdir -p`|
| `rd`     | `rmdir`                |
| `-`     | `cd "$OLDPWD"`                |
| `..`     | `cd ..`                |
| `....`   | `cd ../..`             |
| `......` | `cd ../../..`          |
| `t`      | `tere --filter-search` |
| `hib`    | `systemctl hibernate`  |

## Install

### Arch Linux
```sh
# Install zsh and some plugins
pacman -S zsh zsh-completions zsh-autosuggestions fzf zsh-syntax-highlighting

# Install the following plugin from AUR
# git-prompt.zsh

# Make Zsh your default shell
chsh -s $(which zsh)

# Create or update your ~/.zshrc according to the config in this repository
# After making changes to your config, update your running Zsh instance
source ~/.zshrc
```

## Benchmarking

I've profiled the startup time on my old 2 core laptop and it takes about 60ms. Thus, you won't notice any startup lag at all with this zsh config. To run this yourself, load the zprof mod at the beginning of your .zshrc (`zmodload zsh/zprof`) and run `zprof` at the end of the file.

```
num  calls                time                       self            name
-----------------------------------------------------------------------------------
 1)    1          35.34    35.34   67.64%     19.03    19.03   36.42%  compinit
 2)    2          16.31     8.16   31.22%     16.31     8.16   31.22%  compaudit
 3)    1           8.39     8.39   16.06%      8.26     8.26   15.81%  _zsh_highlight_load_highlighters
 4)    1           6.12     6.12   11.71%      6.12     6.12   11.71%  _zsh_highlight_bind_widgets
 5)    1           1.01     1.01    1.94%      1.01     1.01    1.94%  colors
 6)    4           0.75     0.19    1.44%      0.75     0.19    1.44%  add-zsh-hook
 7)    2           0.55     0.28    1.06%      0.55     0.28    1.06%  is-at-least
 8)    1           0.21     0.21    0.41%      0.21     0.21    0.41%  (anon) [/usr/share/zsh/plugins/zsh-autosuggestions/zsh-autosuggestions.zsh:458]
```
