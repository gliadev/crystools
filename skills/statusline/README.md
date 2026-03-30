# Status Line

A two-line powerline-style status line for Claude Code that shows real-time session information.

## Preview

```
 🪟 [▓▓▓32%-------]  📁 myproject  ⎇ main 󰄬  🕐 00:12:34 (00:08:21)
 ⏳[12%--------]  🤖 Opus 4.6 1M  💲 1.23  🔄 TK Cached w/r: 45/120  ⠋
```

## Features

- **Context window** — progress bar with color thresholds (green < 50%, yellow < 75%, red ≥ 75%)
- **Directory** — smart path: `project/…/current` for deep paths
- **Git** — branch, dirty/clean indicator, ahead/behind upstream, lines added/removed
- **Session duration** — total wall time + API time
- **Rate limits** — 5-hour usage bar with reset countdown
- **Model** — current model name + context window size
- **Cost** — running session cost in USD
- **Cache** — tokens written/read from cache
- **Spinner** — animated braille spinner

## Icon Modes

Set the `STATUSLINE_ICONS` environment variable:

| Mode    | Description                                    |
|---------|------------------------------------------------|
| `nerd`  | Nerd Font glyphs (best experience, requires [Nerd Font](https://www.nerdfonts.com/)) |
| `emoji` | Unicode emoji (default, works everywhere)      |
| `none`  | Plain text, no icons                           |

## Setup

Run the skill:

```
/crystools:statusline
```

Or manually add to `~/.claude/settings.json`:

```json
{
  "statusLine": {
    "type": "command",
    "command": "bash /path/to/skills/statusline/statusline-command.sh"
  },
  "env": {
    "STATUSLINE_ICONS": "nerd"
  }
}
```

## Requirements

- `jq` — JSON parser (used to read Claude's status input)
- `git` — for branch and status info
- A [Nerd Font](https://www.nerdfonts.com/) terminal font (only for `nerd` mode)
