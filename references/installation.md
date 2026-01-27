# Installation Guide (Agent-Agnostic)

Use this reference only **after** the user confirms the stack.

## Preferred (source-aware, multi-agent)
Use the Skills CLI only when the skill is known to be supported by it (e.g., discovered via `npx skills find` or listed on skills.sh). Do **not** default to Skills CLI for arbitrary repos.

```bash
npx skills add owner/repo --skill skill-name -a codex -a claude-code -y
```

Notes:
- `-a` targets agents; use `--all` to install to all detected agents.
- If a user wants project-level only, use the agent’s project skills path instead.
- If the skill did **not** come from Skills CLI discovery, use a source-verified install method instead (see below).

## Context7-sourced skills
If a skill came from Context7, follow Context7’s install guidance or CLI output. Do not use `npx skills add` unless the skill is also listed by Skills CLI.

## Codex CLI
Project-level path:
```
<repo>/.codex/skills/<skill-name>/
```

Install via Codex’s built-in skill installer (preferred for repo-based skills):
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

## Fallback (only if verified)
If install methods are unclear, **do not** hand-write or reconstruct a skill. Ask for an authoritative source (official repo, ZIP, or Skills CLI listing) and only install from that source.

If you must manually copy a verified skill, consult `references/agent-skills.md` for agent-specific paths, skill format, and discovery locations.
