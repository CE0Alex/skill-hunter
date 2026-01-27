# Installation Guide (Agent-Agnostic)

Use this reference only **after** the user confirms the stack.

## Preferred (CLI-first, multi-agent)
If the Skills CLI is available, prefer it for installs across agents:

```bash
npx skills add owner/repo --skill skill-name -a codex -a claude-code -y
```

Notes:
- `-a` targets agents; use `--all` to install to all detected agents.
- If a user wants project-level only, use the agent’s project skills path instead.

## Codex CLI
Project-level path:
```
<repo>/.codex/skills/<skill-name>/
```

Install via Codex’s built-in skill installer:
```
$skill-installer install https://github.com/owner/repo/tree/main/path/to/skill
```

Or describe it:
```
$skill-installer install the <skill-name> skill from owner/repo
```

Manual install:
```
mkdir -p .codex/skills
cp -R skill-name .codex/skills/
```

**Note:** Restart Codex after installing new skills.

## Claude Code (CLI)
Project-level (recommended):
```
<repo>/.claude/skills/<skill-name>/
```

Global:
```
~/.claude/skills/<skill-name>/
```

GitHub install:
```bash
# Project-level
mkdir -p .claude/skills && git clone https://github.com/owner/repo-name.git .claude/skills/skill-name

# Global
mkdir -p ~/.claude/skills && git clone https://github.com/owner/repo-name.git ~/.claude/skills/skill-name
```

## Claude (Web/Desktop)
Package the skill folder as a ZIP and upload via **Settings > Capabilities**.

## Other Clients
Ask for the official project-level skills path or CLI. If no official guidance exists, present a best-effort option and mark it unverified.
