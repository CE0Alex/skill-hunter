# Skill Hunter

Agent skill to analyze a repo and recommend a best-fit skill stack with verified sources.

## Compatibility

This skill follows the Agent Skills format (`SKILL.md` with YAML frontmatter) and is designed to work across multiple AI coding agents. It includes agent-specific tool mappings so the instructions work whether you're using Claude Code, Codex CLI, or other compatible clients.

### Tested Agents
| Agent | Version Tested | Status | Core Tools |
|-------|----------------|--------|------------|
| Claude Code (CLI) | 2.1.19 | ✅ Supported | `WebSearch`, `Glob`, `Grep`, `Read`, `Bash`, `Edit` |
| Codex CLI | 0.91.0 | ✅ Supported | `web.run`, `functions.exec_command`, `functions.apply_patch` |
| Claude (Web/Desktop) | — | ✅ Supported | Upload as ZIP |

> **Note**: Tool names and availability may change between versions. This skill was last verified on 2025-01-26.

## What it does
- Scans a project and builds a concise dossier (stack, workflows, constraints).
- Searches skills registries and inspects candidates before recommending them.
- Prefers official or trusted sources and flags unproven skills as optional.
- Recommends a minimal stack and installs only after confirmation.

## When to use
- "Find the best skills for this project"
- "Analyze this codebase and recommend a skill stack"

## Install

### Claude Code (CLI)
Claude Code discovers skills from:
- **Personal (global)**: `~/.claude/skills/<skill-name>/`
- **Project-level**: `.claude/skills/<skill-name>/` (in the project root)
- Plugin skills: bundled with installed plugins

```bash
# Global install (available in all projects)
mkdir -p ~/.claude/skills/skill-hunter
cp SKILL.md ~/.claude/skills/skill-hunter/

# Or project-level install
mkdir -p .claude/skills/skill-hunter
cp SKILL.md .claude/skills/skill-hunter/
```

Note: `allowed-tools` frontmatter is supported only in Claude Code.

### Claude (Web/Desktop)
Upload the skill as a ZIP via Settings > Capabilities.
Requires Skills and Code Execution to be enabled (org admins may need to enable it first).

### Codex CLI
Project-level path under the repo root:
```bash
mkdir -p .codex/skills/skill-hunter
cp SKILL.md .codex/skills/skill-hunter/
```

Or use the skill installer if available:
```bash
python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo CE0Alex/skill-hunter --dest ./.codex/skills
```

### Generic (any skills-enabled client)
- Place the `skill-hunter/` folder in the project-level skills directory for your client, or
- Import/upload the skill as a ZIP if your client uses a UI.

If unsure where your client expects skills, check its documentation for the project-level skills path or import flow.

## Tool Requirements

This skill requires web access for searching skill registries. The skill includes a tool mapping table so it adapts to the tools available in your agent:

| Task | Claude Code | Codex CLI |
|------|-------------|-----------|
| Web search | `WebSearch` | `web.run` |
| Find files | `Glob` | `functions.exec_command` + `find`/`rg --files` |
| Search contents | `Grep` | `functions.exec_command` + `rg -n` |
| Read files | `Read` | `functions.exec_command` + `cat` |
| Shell commands | `Bash` | `functions.exec_command` |
| Edit files | `Edit` / `Write` | `functions.apply_patch` |
| Ask user | `AskUserQuestion` | `functions.request_user_input` |

## Usage (example)
"Please use Skill Hunter to find the best skills to work on this project."

## Structure
```
skill-hunter/
├── SKILL.md      # The skill definition
├── README.md     # This file
└── LICENSE       # MIT license
```

## License
MIT
