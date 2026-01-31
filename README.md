# Skill Hunter

An agent skill that analyzes your project and recommends a curated stack of **external skills** from trusted registries.

## What It Does

Skill Hunter helps you discover and install the best skills for your project:

1. **Analyzes your project** — scans your codebase to understand the stack, workflows, and constraints
2. **Asks clarifying questions** — confirms your goals, trust preferences, and category focus before searching
3. **Searches skill registries** — queries Context7, skills.sh, and GitHub for relevant skills
4. **Inspects candidates** — verifies each skill's source, maintainer, and compatibility
5. **Recommends a stack** — presents a minimal set of skills with confidence ratings and tradeoffs
6. **Installs after confirmation** — only installs skills you approve, using verified methods

For the complete workflow and rules, see [SKILL.md](SKILL.md).

## When to Use

Invoke Skill Hunter when you want to find **new external skills**:
- "Find the best skills for this project"
- "Recommend external skills for TypeScript testing"
- "What skills exist for CI/CD automation?"

**Do not use** for questions about already-installed skills — Skill Hunter is for discovery, not usage guidance.

## Compatibility

This skill follows the [Agent Skills](https://agentskills.io) format and works with any agent that supports skills.

### Tested Agents
| Agent | Version Tested | Status |
|-------|----------------|--------|
| Claude Code (CLI) | 2.1.19 | ✅ Supported |
| Codex CLI | 0.91.0 | ✅ Supported |
| Claude (Web/Desktop) | — | ✅ Supported (ZIP upload) |

### Other Agents
Skill Hunter supports 50+ agents via the [Skills CLI registry](https://github.com/vercel-labs/skills). See [references/agent-skills.md](references/agent-skills.md) for the full list of supported agents and their skill paths.

## Installing Skill Hunter

These instructions are for installing **Skill Hunter itself** as a skill in your agent. Once installed, you can invoke Skill Hunter to discover and install other skills for your project.

### Generic (Any Skills-Enabled Agent)

Copy the entire `skill-hunter/` folder to your agent's project-level skills directory, or upload it as a ZIP if your agent uses a UI-based import.

If you're unsure where your agent expects skills, check [references/agent-skills.md](references/agent-skills.md) for the full list of agent paths, or consult your agent's documentation.

### Claude Code (CLI)

```bash
# Project-level (recommended)
mkdir -p .claude/skills
cp -R skill-hunter .claude/skills/

# Or global (available in all projects)
mkdir -p ~/.claude/skills
cp -R skill-hunter ~/.claude/skills/
```

### Codex CLI

```bash
mkdir -p .codex/skills
cp -R skill-hunter .codex/skills/
```

Or use the built-in skill installer:
```
$skill-installer install the skill-hunter skill from owner/repo-name
```

> **Note:** Restart Codex after installing new skills.

### Claude (Web/Desktop)

Upload the skill as a ZIP via **Settings > Capabilities**. Skills and Code Execution must be enabled.

### Other Agents

See [references/agent-skills.md](references/agent-skills.md) for paths and installation methods for 50+ supported agents.

---

## How Skill Hunter Installs Discovered Skills

Once Skill Hunter is installed and you invoke it, it uses these tools to find and install skills for your project:

| Tool | Purpose |
|------|---------|
| [Skills CLI](https://skills.sh) (`npx skills`) | Primary discovery and installation |
| [Context7 CLI](https://context7.com) (`ctx7`) | Secondary registry search |
| GitHub search | Fallback for gaps not in registries |

Skill Hunter handles the installation commands automatically after you confirm the recommended stack. For the full CLI reference used internally, see [references/installation.md](references/installation.md).

## Repo Structure

| File | Purpose |
|------|---------|
| `SKILL.md` | The skill itself — workflow rules and instructions for the agent |
| `README.md` | This file — user documentation |
| `AGENTS.md` | Contributor guide for maintaining Skill Hunter |
| `references/installation.md` | Agent reference: CLI commands for installing discovered skills |
| `references/agent-skills.md` | Agent reference: paths, formats, and supported agents |

## License

MIT
