# Crystools

Claude Code plugin with productivity tools: status line, utilities, and workflow enhancements.

## Available Commands

| Command | Description |
|---------|-------------|
| `/crystools:statusline` | Configure a two-line powerline-style status bar with context, git, cost, rate limits, and cache info |

## Install

> **Note:** This plugin has been submitted to the official Claude Code marketplace. Until it's approved, install it manually:

```bash
claude plugin marketplace add crystian/crystools
claude plugin install crystools@crystian-marketplace
```

Then inside Claude Code, run `/crystools:statusline` to set up the status line.

### Permissions

During setup, Claude Code will ask for permission to:

- **Read** `~/.claude/settings.json` — to check if the status line is already configured
- **Edit** `~/.claude/settings.json` — to add the `statusLine` and `CRYSTOOLS_SL_ICONS` configuration
- **Bash (find)** — to locate the [`statusline-command.sh`](./scripts/statusline-command.sh) script in the plugin installation directory

## Status Line Preview

Supports three icon modes: **nerd**, **emoji** (default), and **none** (plain text).



## Nerd Font

Install some Nerd Font from the [Nerd Font](https://www.nerdfonts.com/) on your system, and configure your terminal to use it. The status line will automatically use the appropriate icons when `CRYSTOOLS_SL_ICONS` is set to `nerd`.

## License

MIT

---

Made with <3 by [Crystian](https://github.com/crystian)
