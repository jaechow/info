# Contributing to info

Thanks for your interest in contributing! This project is a curated CLI command reference — quality and accuracy matter more than quantity.

## How to Contribute

1. **Fork** the repository
2. **Create a branch** for your addition (`git checkout -b add-docker-prune`)
3. **Make your changes** following the style guide below
4. **Submit a pull request** with a clear description of what you added or changed

## Style Guide

### Command entries should include:

- A one-line description of what the command does
- The command in a fenced code block with the appropriate language tag
- Installation instructions if the tool isn't built-in

### Example format:

```markdown
- Search file contents recursively with `ripgrep`

\`\`\`shell
rg "pattern" --type py
\`\`\`

> Install: `brew install ripgrep`
```

### Do:

- Verify every command works before submitting
- Use the simplest form of a command that gets the job done
- Include the OS/platform if a command is platform-specific
- Add a "Last verified" note for version-sensitive commands

### Don't:

- Add commands that are easily found in `--help` output
- Include long tutorial-style explanations (link to docs instead)
- Submit commands with hardcoded paths or credentials
- Duplicate commands already covered in another section

## Sections

Each section lives in its own file. If you're adding commands to an existing section, edit that file. If you're proposing a new section, open an issue first to discuss.

## Reporting Issues

Found a broken command or outdated version? Open an issue with:
- The command that's broken
- Your OS and shell version
- What you expected vs. what happened

## License

By contributing, you agree that your contributions will be licensed under the MIT License.
