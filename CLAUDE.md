# Crystools Plugin

## Project Overview

Claude Code plugin with productivity tools: status line, utilities, and workflow enhancements.

## Repository Structure

```
skills/           — each subdirectory is one skill
  <name>/
    SKILL.md      — skill definition (frontmatter + instructions)
    README.md     — user-facing docs
    references/   — supporting material loaded on demand
.claude-plugin/
  plugin.json     — plugin manifest (name, version, description)
hooks/
  pre-commit      — interactive version bump for plugin.json + SKILL.md files
setup.sh          — configures git to use hooks/ directory
```

## Setup

```bash
./setup.sh   # sets git core.hooksPath to hooks/
```

## Documentation

- All documentation must be written in English.

## Version Management

Versions are managed via the pre-commit hook — it prompts for patch/minor/major bump on each commit and updates both `.claude-plugin/plugin.json` and all `SKILL.md` frontmatter `version:` fields in sync. Never bump versions manually or programmatically outside this hook.

## SKILL.md Conventions

- **Frontmatter** (YAML between `---`):
  - `name` (required): lowercase, hyphens only, 1-64 characters.
  - `author` (required): author name.
  - `license` (required): license identifier (e.g., `MIT`).
  - `description` (required): max 1024 chars, third person, with specific trigger phrases.
  - `metadata` (required): nested object with:
    - `version`: semver, managed by pre-commit hook — never set manually.
    - `tags`: comma-separated keywords for discoverability.
    - `github`: repository URL.
    - `linkedin`: author's LinkedIn URL.
- **Body**: under 500 lines / ~5k tokens. Overflow goes to `references/` subdirectory.
- **References**: markdown files in `references/` loaded on demand, referenced from the body with explicit load instructions.

## Pre-commit Hook

The hook at `hooks/pre-commit` is interactive (reads from `/dev/tty`) — it cannot run in non-interactive contexts. It bumps the version in `plugin.json` and propagates to matching SKILL.md files. When committing from Claude Code, the user will need to handle the interactive prompt or skip with `s`.

## Git

**NEVER run `git push`.** Pushing is done manually by the user.

**NEVER commit automatically.** Do NOT commit after finishing work unless the user explicitly asks. Completing tasks ≠ commit.
