# Shell & Productivity

Terminal setup, shell customization, and session management.

## Starship Prompt

Minimal, fast, cross-shell prompt with git integration:

```shell
eval "$(starship init zsh)"
```

Create a config file:

```shell
mkdir -p ~/.config && starship preset pure-preset -o ~/.config/starship.toml
```

> Install: `brew install starship` · `cargo install starship` · `winget install Starship.Starship`

---

## Zsh Plugins

### zsh-autosuggestions

Fish-like autosuggestions as you type:

```shell
brew install zsh-autosuggestions
echo "source $(brew --prefix)/share/zsh-autosuggestions/zsh-autosuggestions.zsh" >> ~/.zshrc
```

### zsh-syntax-highlighting

Real-time command validation with color:

```shell
brew install zsh-syntax-highlighting
echo "source $(brew --prefix)/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" >> ~/.zshrc
```

---

## tmux

Start a new named session:

```shell
tmux new -s work
```

Detach from a session:

++ctrl+b++ then ++d++

List sessions:

```shell
tmux ls
```

Reattach to a session:

```shell
tmux attach -t work
```

### Common Key Bindings

All prefixed with ++ctrl+b++:

| Keys | Action |
|------|--------|
| `"` | Split pane horizontally |
| `%` | Split pane vertically |
| Arrow keys | Switch between panes |
| `c` | Create new window |
| `n` / `p` | Next / previous window |
| `z` | Toggle pane zoom (fullscreen) |
| `d` | Detach session |

---

## Useful Shell Functions

Add to `~/.zshrc` or `~/.bashrc`:

### `mkcd` — create and enter a directory

```shell
mkcd() { mkdir -p "$1" && cd "$1"; }
```

### `extract` — universal archive extractor

```shell
extract() {
  case "$1" in
    *.tar.bz2) tar xjf "$1" ;;
    *.tar.gz)  tar xzf "$1" ;;
    *.tar.xz)  tar xJf "$1" ;;
    *.zip)     unzip "$1" ;;
    *.gz)      gunzip "$1" ;;
    *.7z)      7z x "$1" ;;
    *)         echo "unsupported: $1" ;;
  esac
}
```

---

## Dotfile Management

Track your config files with a bare git repo:

```shell
git init --bare $HOME/.dotfiles
alias dotfiles='git --git-dir=$HOME/.dotfiles --work-tree=$HOME'
dotfiles config --local status.showUntrackedFiles no
```

Add files:

```shell
dotfiles add ~/.zshrc ~/.gitconfig
dotfiles commit -m "add shell config"
dotfiles remote add origin git@github.com:user/dotfiles.git
dotfiles push -u origin main
```
