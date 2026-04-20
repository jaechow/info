# info

**The curated CLI command reference for developers.**

Stop googling the same commands. Bookmark this instead.

---

## Sections

| Section | What's inside |
|---------|---------------|
| [CLI Power Tools](cli-tools.md) | Modern replacements for grep, find, cat, ls, and cd |
| [Git](git.md) | Beyond the basics — rebase, bisect, worktrees, `gh` CLI |
| [Docker](docker.md) | Build, run, compose, prune — the commands you actually use |
| [AI CLI Tools](ai-tools.md) | Claude Code, GitHub Copilot CLI, and other AI-assisted workflows |
| [Shell & Productivity](shell.md) | zsh, starship, tmux, and dotfile essentials |
| [Networking & Security](networking.md) | curl, ssh, openssl, and debugging network issues |
| [Cloud CLI](cloud.md) | AWS, GCP, Azure, kubectl, and terraform quick reference |
| [macOS Power User](macos.md) | Homebrew, defaults write, system utilities |
| [Package Managers](package-managers.md) | winget, brew, scoop, nix, mise — cross-platform |
| [Node.js & JS Toolchain](node.md) | npm, pnpm, bun, npx, tsx, and debugging |

---

## Quick Start

Install the tools that make everything else faster:

=== "macOS"

    ```shell
    brew install ripgrep fd bat eza zoxide fzf jq
    ```

=== "Linux"

    ```shell
    sudo apt install ripgrep fd-find bat fzf jq
    # eza and zoxide via cargo or binary releases
    cargo install eza zoxide
    ```

=== "Windows"

    ```shell
    winget install BurntSushi.ripgrep sharkdp.fd sharkdp.bat eza-community.eza ajeetdsouza.zoxide junegunn.fzf jqlang.jq
    ```

---

## Contributing

Found a better way? Missing a command you use daily? See the [contributing guide](https://github.com/jaechow/info/blob/main/CONTRIBUTING.md).
