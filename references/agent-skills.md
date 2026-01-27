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

Note: Gemini CLI uses the Skills CLI agent id `gemini-cli` and installs to `.gemini/skills/` at the project level.

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

Spec highlights (Agent Skills):
- `name`: max 64 chars; lowercase letters, numbers, hyphens; must not start/end with a hyphen.
- `description`: max 1024 chars; non‑empty; describe what the skill does and when to use it.
- Optional frontmatter fields commonly used: `license`, `metadata`, `compatibility`, `allowed-tools`.
- Optional directories: `scripts/`, `references/`, `assets/` (include them when copying a skill).

Optional (Skills CLI‑specific):
- `metadata.internal: true` hides the skill from default discovery; only visible when internal skills are enabled.

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

## Multi‑skill repos and shared files

- If the source repo contains multiple skills **or** you are installing a specific skill by name, list available skills first (Skills CLI `--list` or the repo’s `skills/` index) and install only the selected skill.
- Manual copy fallback applies **only** when the user explicitly requests a skill from that repo and the exact files can be verified.
- Copy the **entire** skill folder plus any shared files explicitly referenced in the skill’s docs. If shared dependencies are unclear, stop and request authoritative install guidance.

## Compatibility

Skills follow the Agent Skills specification, but some features can be agent‑specific. This table reflects feature support reported by the Skills CLI ecosystem at time of writing:

| Feature         | OpenCode | OpenHands | Claude Code | Cline | CodeBuddy | Codex | Command Code | Kiro CLI | Cursor | Antigravity | Roo Code | GitHub Copilot | Amp | Clawdbot | Neovate | Pi | Qoder | Zencoder |
| --------------- | -------- | --------- | ----------- | ----- | --------- | ----- | ------------ | -------- | ------ | ----------- | -------- | -------------- | --- | -------- | ------- | -- | ----- | -------- |
| Basic skills    | Yes      | Yes       | Yes         | Yes   | Yes       | Yes   | Yes          | Yes      | Yes    | Yes         | Yes      | Yes            | Yes | Yes      | Yes     | Yes | Yes   | Yes      |
| `allowed-tools` | Yes      | Yes       | Yes         | Yes   | Yes       | Yes   | Yes          | No       | Yes    | Yes         | Yes      | Yes            | Yes | Yes      | Yes     | Yes | Yes   | No       |
| `context: fork` | No       | No        | Yes         | No    | No        | No    | No           | No       | No     | No          | No       | No             | No  | No       | No      | No | No    | No       |
| Hooks           | No       | No        | Yes         | Yes   | No        | No    | No           | No       | No     | No          | No       | No             | No  | No       | No      | No | No    | No       |

## Troubleshooting

- **No skills found**: ensure `SKILL.md` contains valid YAML frontmatter with `name` and `description`.
- **Skill not loading**: confirm the target path is correct and restart the agent if required.
- **Permission errors**: verify write access to the target directory.

## Environment Variables (Skills CLI)

- `INSTALL_INTERNAL_SKILLS=1` to show/install skills marked `metadata.internal: true`
- `DISABLE_TELEMETRY=1` or `DO_NOT_TRACK=1` to disable telemetry (if supported by CLI)

## Telemetry

The Skills CLI may collect anonymous usage data to improve the tool. Telemetry is typically disabled in CI environments.

## Related Links

Prefer official docs for the current agent and the Agent Skills spec when available.

- Agent Skills Specification: https://agentskills.io
- Skills Directory: https://skills.sh
- Amp Skills Documentation: https://ampcode.com/manual#agent-skills
- Antigravity Skills Documentation: https://antigravity.google/docs/skills
- Factory AI / Droid Skills Documentation: https://docs.factory.ai/cli/configuration/skills
- Claude Code Skills Documentation: https://code.claude.com/docs/en/skills
- Clawdbot Skills Documentation: https://docs.clawd.bot/tools/skills
- Cline Skills Documentation: https://docs.cline.bot/features/skills
- CodeBuddy Skills Documentation: https://www.codebuddy.ai/docs/ide/Features/Skills
- Codex Skills Documentation: https://developers.openai.com/codex/skills
- Command Code Skills Documentation: https://commandcode.ai/docs/skills
- Crush Skills Documentation: https://github.com/charmbracelet/crush?tab=readme-ov-file#agent-skills
- Cursor Skills Documentation: https://cursor.com/docs/context/skills
- Gemini CLI Skills Documentation: https://geminicli.com/docs/cli/skills/
- GitHub Copilot Agent Skills: https://docs.github.com/en/copilot/concepts/agents/about-agent-skills
- Kiro CLI Skills Documentation: https://kiro.dev/docs/cli/custom-agents/configuration-reference/#skill-resources
- OpenCode Skills Documentation: https://opencode.ai/docs/skills
- Qwen Code Skills Documentation: https://qwenlm.github.io/qwen-code-docs/en/users/features/skills/
- OpenHands Skills Documentation: https://docs.openhands.ai/modules/usage/how-to/using-skills
- Pi Skills Documentation: https://github.com/badlogic/pi-mono/blob/main/packages/coding-agent/docs/skills.md
- Qoder Skills Documentation: https://docs.qoder.com/cli/Skills
- Roo Code Skills Documentation: https://docs.roocode.com/features/skills
- Trae Skills Documentation: https://docs.trae.ai/ide/skills
- Vercel Agent Skills Repository: https://github.com/vercel-labs/agent-skills
