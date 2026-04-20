# Package Managers

Install, update, and manage software across platforms.

## Homebrew (macOS / Linux)

Install Homebrew:

```shell
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Search for a package:

```shell
brew search node
```

Install a CLI tool vs. a GUI app:

```shell
brew install node          # CLI formula
brew install --cask firefox  # GUI cask
```

See what's outdated:

```shell
brew outdated
```

Upgrade everything:

```shell
brew upgrade
```

---

## winget (Windows)

Search for a package:

```shell
winget search "Visual Studio Code"
```

Install:

```shell
winget install Microsoft.VisualStudioCode
```

Upgrade all installed packages:

```shell
winget upgrade --all
```

Export installed packages:

```shell
winget export -o packages.json
```

Import on a new machine:

```shell
winget import -i packages.json
```

> Built into Windows 11. Windows 10 users: install via [Microsoft Store](https://apps.microsoft.com/detail/9nblggh4nns1).

---

## Scoop (Windows)

Installs to user directory — no admin required:

```shell
irm get.scoop.sh | iex
```

Add the extras bucket for more packages:

```shell
scoop bucket add extras
```

Install and manage:

```shell
scoop install git nodejs python
scoop update *
```

> Best for dev tools. Use winget for GUI apps.

---

## Nix (Cross-Platform)

Install Nix:

```shell
sh <(curl -L https://nixos.org/nix/install)
```

Run a tool without installing it:

```shell
nix run nixpkgs#cowsay -- "hello"
```

Enter a shell with specific tools available:

```shell
nix shell nixpkgs#nodejs nixpkgs#python3
```

!!! tip
    Nix guarantees reproducible environments. Great for CI and shared dev setups.

---

## mise (Runtime Version Manager)

Replaces `nvm`, `pyenv`, `rbenv`, `goenv` with a single tool:

```shell
mise use node@22
mise use python@3.12
```

Install a specific version:

```shell
mise install node@22.0.0
```

List installed runtimes:

```shell
mise ls
```

Set a global default:

```shell
mise use --global node@22
```

Project-local versions (creates `.mise.toml`):

```shell
mise use node@20
```

> Install: `brew install mise` · `cargo install mise` · `curl https://mise.run | sh`

---

## Comparison

| Feature | Homebrew | winget | Scoop | Nix | mise |
|---------|----------|--------|-------|-----|------|
| **Platform** | macOS, Linux | Windows | Windows | Cross-platform | Cross-platform |
| **Best for** | General packages | GUI + CLI apps | Dev tools (no admin) | Reproducible envs | Runtime versions |
| **Admin required** | No | Sometimes | No | No | No |
