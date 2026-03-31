---
description: Configure Claude Code status line with context, git, cost, rate limits, and cache info.
allowed-tools: Read, Edit, Bash(grep:*), Bash(find:*)
---

# Status Line Setup

First, read `~/.claude/settings.json` and check if `statusLine` is already configured.

## If already installed

Tell the user the status line is already configured and ask:
1. Reinstall (reconfigure)
2. Uninstall (remove status line)
3. Cancel

If **uninstall**: remove the `statusLine` key and the `CRYSTOOLS_SL_ICONS` key from `env` in `~/.claude/settings.json`, preserving all other keys. Confirm removal and tell the user to restart Claude Code.

If **cancel**: do nothing and stop.

If **reinstall**: continue with the setup procedure below.

## If not installed

Inform the user:

> This command will configure your Claude Code status line by modifying `~/.claude/settings.json`.
> It will point to a bash script (`statusline-command.sh`) bundled with this plugin that runs on every status line refresh.
> You can review the script source here: https://github.com/crystian/crystools/blob/main/scripts/statusline-command.sh
> You will be asked for permission before any file is modified.

Then show a preview of how the status line will look (emoji mode):

```
 🪟 [▓▓▓32%-------]  📁 myproject  ⎇ main 󰄬 +12 -3  🕐 00:12:34 (00:08:21)
 ⏳[12%--------]  🤖 Opus 4.6 1M  💲 1.23  🔄 TK Cached w/r: 45/120  ⠋
```

Explain what each segment shows:
- 🪟 **Context window** — usage progress bar with color thresholds (green < 50%, yellow < 75%, red >= 75%)
- 📁 **Directory** — smart project path (deep paths show `project/…/current`)
- ⎇ **Git** — branch name, dirty/clean indicator, ahead/behind upstream, lines added/removed
- 🕐 **Duration** — session wall time + API time in parentheses
- ⏳ **Rate limit** — 5-hour usage bar with reset countdown
- 🤖 **Model** — current model + context window size
- 💲 **Cost** — running session cost in USD
- 🔄 **Cache** — tokens written/read from cache

Wait for the user to confirm before proceeding. If the user declines, do nothing and stop.

## Setup procedure

1. **Detect the platform** and find the script:
   - **Linux/macOS**: find `statusline-command.sh`
   - **Windows**: find `statusline-command.ps1`

   ```bash
   # Linux/macOS
   find ~/.claude -name "statusline-command.sh" -path "*/scripts/*" 2>/dev/null | head -1
   ```
   ```powershell
   # Windows
   Get-ChildItem -Path "$env:USERPROFILE\.claude" -Recurse -Filter "statusline-command.ps1" | Select-Object -First 1 -ExpandProperty FullName
   ```
   If not found, ask the user for the plugin location.

2. **Read current settings** from `~/.claude/settings.json`.

3. **Ask the user which icon mode they prefer** (if `CRYSTOOLS_SL_ICONS` is not already set):

   | Value   | Description                          |
   |---------|--------------------------------------|
   | `nerd`  | Nerd Font icons (requires a [Nerd Font](https://www.nerdfonts.com/) terminal) |
   | `emoji` | Unicode emoji fallback (default)     |
   | `none`  | Plain text, no icons                 |

4. **Set the `statusLine` and `env` config** in `~/.claude/settings.json`, preserving all existing keys:
   - **Linux/macOS**:
   ```json
   {
     "statusLine": {
       "type": "command",
       "command": "bash <ABSOLUTE_PATH>/statusline-command.sh"
     },
     "env": {
       "CRYSTOOLS_SL_ICONS": "<user_choice>"
     }
   }
   ```
   - **Windows**:
   ```json
   {
     "statusLine": {
       "type": "command",
       "command": "powershell -File <ABSOLUTE_PATH>/statusline-command.ps1"
     },
     "env": {
       "CRYSTOOLS_SL_ICONS": "<user_choice>"
     }
   }
   ```

5. **Confirm** the setup is complete and tell the user to restart Claude Code to see the status line.

## Uninstall

To remove: delete the `statusLine` key and the `CRYSTOOLS_SL_ICONS` env var from `~/.claude/settings.json`.

## Requirements

- `jq` must be installed (used by the script to parse JSON input)
- `git` for branch/status info
- A Nerd Font-compatible terminal if using `nerd` icon mode
