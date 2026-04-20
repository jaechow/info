# Git

Beyond `add`, `commit`, `push`. The commands that save you when things go sideways.

## Interactive Rebase

Rewrite the last 5 commits (reorder, squash, edit messages):

```shell
git rebase -i HEAD~5
```

!!! warning
    Never rebase commits that have been pushed to a shared branch.

---

## Bisect

Find the commit that introduced a bug using binary search:

```shell
git bisect start
git bisect bad                  # current commit is broken
git bisect good v1.2.0          # this tag was working
# Git checks out a middle commit — test it, then:
git bisect good                 # or: git bisect bad
# Repeat until Git identifies the first bad commit
git bisect reset                # return to original HEAD
```

---

## Worktrees

Work on multiple branches simultaneously without stashing:

```shell
git worktree add ../feature-branch feature-branch
```

List active worktrees:

```shell
git worktree list
```

Remove when done:

```shell
git worktree remove ../feature-branch
```

---

## Reflog — Undo Almost Anything

See every HEAD movement (even after reset):

```shell
git reflog
```

Recover a commit you accidentally reset away:

```shell
git reset --hard HEAD@{3}
```

---

## Stash

Stash with a descriptive name:

```shell
git stash push -m "WIP: auth refactor"
```

List stashes:

```shell
git stash list
```

Apply a specific stash without removing it:

```shell
git stash apply stash@{2}
```

---

## GitHub CLI (`gh`)

Create a PR from the current branch:

```shell
gh pr create --fill
```

Check out a PR locally by number:

```shell
gh pr checkout 42
```

View CI status for the current branch:

```shell
gh pr checks
```

Browse the repo in your browser:

```shell
gh repo view --web
```

Search issues:

```shell
gh issue list --label "bug" --state open
```

> Install: `brew install gh` · `winget install GitHub.cli`

---

## Useful Aliases

Add to `~/.gitconfig` under `[alias]`:

```ini
[alias]
    lg = log --oneline --graph --all --decorate
    co = checkout
    br = branch -vv
    st = status -sb
    undo = reset --soft HEAD~1
    amend = commit --amend --no-edit
    wip = !git add -A && git commit -m "WIP"
```

---

## Log Tricks

Commits by a specific author in the last week:

```shell
git log --author="jason" --since="1 week ago" --oneline
```

Show files changed in each commit:

```shell
git log --stat --oneline -10
```

Search commit messages:

```shell
git log --grep="fix auth" --oneline
```
