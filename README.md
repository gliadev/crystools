# Crystools

Claude Code plugin with productivity tools: status line, utilities, and workflow enhancements.

## Available Skills

| Skill | Description | Docs |
|-------|-------------|------|
| [statusline](./skills/statusline/) | Two-line powerline-style status bar with context, git, cost, rate limits, and cache info | [README](./skills/statusline/README.md) |

## Install

```bash
claude /plugin install crystian/crystools    # Claude Code plugin
```

Plugin namespace: `/crystools:<skill-name>`

## Setup

After cloning (contributors):

```bash
./setup.sh   # configures git hooks for version bump on each commit
```

## License

MIT

---

Made by [Crystian](https://github.com/crystian)
