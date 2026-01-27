# Agent Skills Reference (Install Paths + Format)

Use this reference only **after** a skill source has been verified (official repo, Skills CLI listing, or vendor-provided ZIP). Do **not** reconstruct skills by hand—only copy the exact skill folder and all required files from the source.

## Supported Agents (Skills CLI registry)

Skills can be installed to these agents. Paths shown are project‑level and global locations.

| Agent | `--agent` | Project Path | Global Path |
|-------|-----------|--------------|-------------|
| Amp | `amp` | `.agents/skills/` | `~/.config/agents/skills/` |
| Antigravity | `antigravity` | `.agent/skills/` | `~/.gemini/antigravity/global_skills/` |
| Claude Code | `claude-code` | `.claude/skills/` | `~/.claude/skills/` |
| Clawdbot | `clawdbot` | `skills/` | `~/.clawdbot/skills/` |
| Cline | `cline` | `.cline/skills/` | `~/.cline/skills/` |
| CodeBuddy | `codebuddy` | `.codebuddy/skills/` | `~/.codebuddy/skills/` |
| Codex | `codex` | `.codex/skills/` | `~/.codex/skills/` |
| Command Code | `command-code` | `.commandcode/skills/` | `~/.commandcode/skills/` |
| Continue | `continue` | `.continue/skills/` | `~/.continue/skills/` |
| Crush | `crush` | `.crush/skills/` | `~/.config/crush/skills/` |
| Cursor | `cursor` | `.cursor/skills/` | `~/.cursor/skills/` |
| Droid | `droid` | `.factory/skills/` | `~/.factory/skills/` |
| Gemini CLI | `gemini-cli` | `.gemini/skills/` | `~/.gemini/skills/` |
| GitHub Copilot | `github-copilot` | `.github/skills/` | `~/.copilot/skills/` |
| Goose | `goose` | `.goose/skills/` | `~/.config/goose/skills/` |
| Kilo Code | `kilo` | `.kilocode/skills/` | `~/.kilocode/skills/` |
| Kiro CLI | `kiro-cli` | `.kiro/skills/` | `~/.kiro/skills/` |
| MCPJam | `mcpjam` | `.mcpjam/skills/` | `~/.mcpjam/skills/` |
| Mux | `mux` | `.mux/skills/` | `~/.mux/skills/` |
| OpenCode | `opencode` | `.opencode/skills/` | `~/.config/opencode/skills/` |
| OpenHands | `openhands` | `.openhands/skills/` | `~/.openhands/skills/` |
| Pi | `pi` | `.pi/skills/` | `~/.pi/agent/skills/` |
| Qoder | `qoder` | `.qoder/skills/` | `~/.qoder/skills/` |
| Qwen Code | `qwen-code` | `.qwen/skills/` | `~/.qwen/skills/` |
| Roo Code | `roo` | `.roo/skills/` | `~/.roo/skills/` |
| Trae | `trae` | `.trae/skills/` | `~/.trae/skills/` |
| Windsurf | `windsurf` | `.windsurf/skills/` | `~/.codeium/windsurf/skills/` |
| Zencoder | `zencoder` | `.zencoder/skills/` | `~/.zencoder/skills/` |
| Neovate | `neovate` | `.neovate/skills/` | `~/.neovate/skills/` |

> If the current agent isn’t listed, installation support is unverified. Ask for official guidance or use the agent’s documented project‑level skills path.

## Creating / Formatting Skills

Skills are directories containing a `SKILL.md` file with YAML frontmatter:

```markdown
---
name: my-skill
description: What this skill does and when to use it
---

# My Skill

Instructions for the agent to follow when this skill is activated.
```

Required frontmatter fields:
- `name` (unique identifier; lowercase + hyphens)
- `description` (when to use the skill)

Optional:
- `metadata.internal: true` to hide from normal discovery (only visible when internal skills are enabled)

## Skill Discovery Locations (Skills CLI)

The Skills CLI looks for skills in these locations in a repo:

- Root (if it contains `SKILL.md`)
- `skills/`
- `skills/.curated/`
- `skills/.experimental/`
- `skills/.system/`
- `.agents/skills/`
- `.agent/skills/`
- `.claude/skills/`
- `skills/`
- `.cline/skills/`
- `.codebuddy/skills/`
- `.codex/skills/`
- `.commandcode/skills/`
- `.continue/skills/`
- `.crush/skills/`
- `.cursor/skills/`
- `.factory/skills/`
- `.gemini/skills/`
- `.github/skills/`
- `.goose/skills/`
- `.kilocode/skills/`
- `.kiro/skills/`
- `.mcpjam/skills/`
- `.mux/skills/`
- `.opencode/skills/`
- `.openhands/skills/`
- `.pi/skills/`
- `.qoder/skills/`
- `.qwen/skills/`
- `.roo/skills/`
- `.trae/skills/`
- `.windsurf/skills/`
- `.zencoder/skills/`
- `.neovate/skills/`

If no skills are found in standard locations, a recursive search is performed.

## Compatibility Notes

Skills follow the Agent Skills specification, but some features can be agent‑specific (for example: `allowed-tools`, `context: fork`, or hooks). If a skill uses agent‑specific features, prefer installation only on compatible agents or document the limitation.

## Troubleshooting

- **No skills found**: ensure `SKILL.md` contains valid YAML frontmatter with `name` and `description`.
- **Skill not loading**: confirm the target path is correct and restart the agent if required.
- **Permission errors**: verify write access to the target directory.

## Environment Variables (Skills CLI)

- `INSTALL_INTERNAL_SKILLS=1` to show/install skills marked `metadata.internal: true`
- `DISABLE_TELEMETRY=1` or `DO_NOT_TRACK=1` to disable telemetry (if supported by CLI)

## Related Links

Prefer official docs for the current agent and the Agent Skills spec when available.
