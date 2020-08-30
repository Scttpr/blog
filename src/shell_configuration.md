# Shell configuration with ZSH-antigen-exa

> This shell configuration is made on Manjaro 20.0

## Setup

Default shell provided with Manjaro is [Bash](https://wiki.archlinux.org/index.php/Bash), it is possible to check it with :
```bash
# Both commands outputs shell path
echo $SHELL
which $SHELL
```

I prefer ZSH because it can be easily bundled and configured with [Oh My Zsh](https://ohmyz.sh/) framework

To install [zsh](https://wiki.archlinux.org/index.php/zsh), in terminal :
```bash
sudo pacman -S zsh
```

Once installed, you can change your shell with `chsh` command :
```bash
# display zsh path
which zsh
# change shell
chsh -s <path_to_zsh>
```

To setup an history for ZSH create a `.histfile` file wherever you wish (I store it in ~/.zsh/.histfile).
Then create `~/.zshrc`, in your favorite text editor :
```bash
HISTFILE=<path_to_your_histfile>
HISTSIZE=1000
SAVEHIST=1000
```

## Antigen & spaceship prompt

### Antigen config
[Antigen](https://evaneos.github.io/le-truc/notes/antigen-le-gestionnaire-de-paquets-pour-zsh) is a package manager for ZSH :
```bash
curl -L git.io/antigen > antigen.zsh
```

And in `~/.zshrc`, following histfile configuration :
```bash
source <path_to_your_.antigen.zsh_file>

# load Oh My ZSH
antigen use oh-my-zsh

# Three bundles I use
antigen bundle zsh-users/zsh-syntax-highlighting
antigen bundle zsh-users/zsh-autosuggestions
antigen bundle zsh-users/zsh-completions

# My favorite shell theme
antigen theme denysdovhan/spaceship-prompt

antigen apply
```

### Spaceship requirements
Once you have your Antigen setup, you need to define a powerline font and an emoji font to fallback on.

I use [Fire Code](https://github.com/tonsky/FiraCode) which supports Powerline since 0.6 as everyday font (shell, IDE, etc).
To fallback and fill emojis I use [Noto emoji](https://github.com/googlefonts/noto-emoji)

In a terminal :
```bash
sudo pacman -S ttf-fira-code noto-fonts-emoji
```

## Exa, a better ls command

I like to install exa and replace basic ls commands.

For exa installation you need to have [Rust](https://rustup.rs/) and Cargo installed, then :
```bash
cargo install exa
```

Then in your `~/.zshrc`, following Antigen configuration :
```bash
# replace basic ls
alias ls="exa"

# display all dir files with tree symbol and rights
alias la="exa -laTL 1"

# Tree command replacement
alias tree="exa -T"
```

## Full configuration
```bash
# hist config
HISTFILE=$HOME/.antigen/.histfile
HISTSIZE=1000
SAVEHIST=1000

# antigen
source $HOME/.antigen/antigen.zsh

antigen use oh-my-zsh

antigen bundle zsh-users/zsh-syntax-highlighting
antigen bundle zsh-users/zsh-autosuggestions
antigen bundle zsh-users/zsh-completions

antigen theme denysdovhan/spaceship-prompt

antigen apply

# aliases
alias ls="exa"
alias la="exa -laTL 1"
alias tree="exa -T"
```

