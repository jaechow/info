# CLI Power Tools

Modern replacements for standard Unix utilities. Faster, more intuitive defaults, and better output.

## ripgrep — faster grep

Recursively search file contents, respecting `.gitignore` by default:

```shell
rg "TODO" --type py
```

Search with context (3 lines before and after):

```shell
rg -C 3 "function.*auth"
```

Search only specific file types:

```shell
rg "import" --type ts --type tsx
```

> Install: `brew install ripgrep` · `apt install ripgrep` · `winget install BurntSushi.ripgrep`

---

## fd — faster find

Find files by name with sensible defaults:

```shell
fd "\.json$" src/
```

Find and delete all `.DS_Store` files:

```shell
fd -H .DS_Store -x rm
```

Find files modified in the last hour:

```shell
fd --changed-within 1h
```

> Install: `brew install fd` · `apt install fd-find` · `winget install sharkdp.fd`

---

## bat — better cat

View files with syntax highlighting and line numbers:

```shell
bat src/index.ts
```

Show only a range of lines:

```shell
bat --line-range 20:40 config.yml
```

Use as a `man` pager:

```shell
export MANPAGER="sh -c 'col -bx | bat -l man -p'"
```

> Install: `brew install bat` · `apt install bat` · `winget install sharkdp.bat`

!!! note "Ubuntu/Debian"
    The binary is installed as `batcat` due to a name conflict. Create an alias: `alias bat='batcat'`

---

## eza — modern ls

List files with git status and icons:

```shell
eza -la --git --icons
```

Tree view with depth limit:

```shell
eza --tree --level=2
```

> Install: `brew install eza` · `cargo install eza` · `winget install eza-community.eza`

---

## zoxide — smarter cd

Jump to a frequently used directory:

```shell
z projects
```

Interactive directory picker (requires fzf):

```shell
zi
```

Add to your shell (put in `.zshrc` or `.bashrc`):

```shell
eval "$(zoxide init zsh)"
```

> Install: `brew install zoxide` · `cargo install zoxide` · `winget install ajeetdsouza.zoxide`

---

## fzf — fuzzy finder

Interactive fuzzy search for anything piped to it:

```shell
find . -type f | fzf
```

Search and open a file in your editor:

```shell
vim $(fzf)
```

Preview files while browsing:

```shell
fzf --preview 'bat --color=always {}'
```

> Install: `brew install fzf` · `apt install fzf` · `winget install junegunn.fzf`

---

## jq — JSON processor

Pretty-print JSON:

```shell
curl -s https://api.example.com/data | jq .
```

Extract a specific field:

```shell
cat data.json | jq '.users[].name'
```

Filter and transform:

```shell
jq '[.items[] | select(.status == "active") | {name, id}]' data.json
```

> Install: `brew install jq` · `apt install jq` · `winget install jqlang.jq`

---

## delta — better git diffs

Configure as your default git diff pager:

```shell
git config --global core.pager delta
git config --global interactive.diffFilter "delta --color-only"
```

Side-by-side view:

```shell
git diff | delta --side-by-side
```

> Install: `brew install git-delta` · `cargo install git-delta`
