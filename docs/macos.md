# macOS Power User

System utilities, Homebrew management, and hidden settings.

## Keyboard Symbols

| Symbol | Key |
|--------|-----|
| ++cmd++ | Command |
| ++option++ | Option |
| ++ctrl++ | Control |
| ++shift++ | Shift |

---

## Homebrew

### Bundle — Reproducible Setup

Export your installed packages to a `Brewfile`:

```shell
brew bundle dump --file=~/Brewfile
```

Install everything from a `Brewfile`:

```shell
brew bundle --file=~/Brewfile
```

### Maintenance

Update Homebrew and all packages:

```shell
brew update && brew upgrade
```

Clean up old versions:

```shell
brew cleanup --prune=all
```

List packages not depended on by anything:

```shell
brew leaves
```

### `mas` — Mac App Store CLI

List installed App Store apps:

```shell
mas list
```

Search and install:

```shell
mas search "Xcode"
mas install 497799835
```

> Install: `brew install mas`

---

## System Utilities

### `caffeinate` — Prevent Sleep

Keep the system awake for 2 hours:

```shell
caffeinate -t 7200
```

Keep awake while a command runs:

```shell
caffeinate -s ./long-running-script.sh
```

### Software Updates

Check for and install all updates:

```shell
softwareupdate --list
softwareupdate --install --all
```

### Disk Utilities

List all disks:

```shell
diskutil list
```

Get SMART status:

```shell
diskutil info disk0 | grep SMART
```

---

## `defaults write` — Hidden Settings

Show all file extensions in Finder:

```shell
defaults write NSGlobalDomain AppleShowAllExtensions -bool true
```

Show hidden files in Finder:

```shell
defaults write com.apple.finder AppleShowAllFiles -bool true
```

Disable the "Are you sure you want to open this application?" dialog:

```shell
defaults write com.apple.LaunchServices LSQuarantine -bool false
```

Speed up Mission Control animations:

```shell
defaults write com.apple.dock expose-animation-duration -float 0.1
```

Speed up SMB network share browsing (skip `.DS_Store` reads):

```shell
defaults write com.apple.desktopservices DSDontWriteNetworkStores -bool TRUE
```

Re-enable default behavior:

```shell
defaults write com.apple.desktopservices DSDontWriteNetworkStores -bool FALSE
```

Restart affected services after changes:

```shell
killall Finder Dock
```

!!! tip
    Read current values first with `defaults read <domain> <key>` before changing them.

---

## Clipboard

Copy a file's contents to clipboard:

```shell
pbcopy < ~/.ssh/id_ed25519.pub
```

Paste clipboard contents to a file:

```shell
pbpaste > output.txt
```

---

## Finder Navigation

| Shortcut | Action |
|----------|--------|
| ++shift+cmd+period++ | Toggle hidden files |
| ++shift+cmd+g++ | Go to folder |
| ++cmd+shift+a++ | Applications folder |
| ++cmd+shift+u++ | Utilities folder |

---

## Quarantine Log

View all downloaded files macOS has tracked:

```shell
sqlite3 ~/Library/Preferences/com.apple.LaunchServices.QuarantineEventsV* \
  'select LSQuarantineDataURLString from LSQuarantineEvent'
```

Clear the log:

```shell
sqlite3 ~/Library/Preferences/com.apple.LaunchServices.QuarantineEventsV* \
  'delete from LSQuarantineEvent'
```
