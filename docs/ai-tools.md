# AI CLI Tools

AI-assisted development from the terminal. Generate commands, explain code, automate tasks.

## Claude Code

Interactive AI coding agent in the terminal:

```shell
claude
```

Start with a specific task:

```shell
claude "refactor auth middleware to use JWT"
```

Run in non-interactive mode for scripting:

```shell
claude -p "explain this error" < error.log
```

Resume the most recent conversation:

```shell
claude --continue
```

> Install: `npm install -g @anthropic-ai/claude-code`

---

## GitHub Copilot CLI

Get command suggestions from natural language:

```shell
gh copilot suggest "find all files larger than 100MB"
```

Explain a command you're unsure about:

```shell
gh copilot explain "tar -xzvf archive.tar.gz"
```

> Install: `gh extension install github/gh-copilot`

---

## llm (Simon Willison)

Send a prompt to any LLM from the terminal:

```shell
llm "write a bash function to retry a command 3 times"
```

Pipe content for analysis:

```shell
cat error.log | llm "summarize the errors and suggest fixes"
```

Use with different models:

```shell
llm -m claude-sonnet-4-6 "review this code for security issues" < auth.py
```

> Install: `pip install llm` · `brew install llm`

---

## Aider

AI pair programming — edits files directly:

```shell
aider src/auth.py src/middleware.py
```

Start with a specific model:

```shell
aider --model claude-sonnet-4-6
```

> Install: `pip install aider-chat`

---

## Pipe Patterns

These patterns work with any AI CLI tool:

Pass a diff for review:

```shell
git diff | claude -p "review this diff for bugs"
```

Generate a commit message:

```shell
git diff --staged | llm "write a concise commit message for these changes"
```

Explain a complex command:

```shell
echo "find . -name '*.log' -mtime +30 -exec gzip {} \;" | gh copilot explain
```
