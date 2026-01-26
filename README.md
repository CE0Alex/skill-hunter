# Skill Hunter

Agent skill to analyze a repo and recommend a best-fit skill stack with verified sources.

## Compatibility

This skill follows the Agent Skills format (`SKILL.md` with YAML frontmatter) and is designed to work across multiple AI coding agents that support skills.

### Tested agents
| Agent | Version tested | Status |
|-------|----------------|--------|
| Claude Code (CLI) | 2.1.19 | ✅ Supported |
| Codex CLI | 0.91.0 | ✅ Supported |
| Claude (Web/Desktop) | — | ✅ Supported (ZIP upload) |

> Last verified: 2026-01-26

## What it does
- Scans a project and builds a concise dossier (stack, workflows, constraints).
- Asks clarifying questions and trust tier preferences before any external search.
- Does **not** ask about browsing if the client already has browsing enabled; only asks if browsing is explicitly disabled/denied.
- If required inputs are missing, asks questions only and does not present candidates or recommendations.
- When external browsing is permitted and available, requires a concise search log and inspection notes before recommendations.
- Recommendations are based on **external skills only**; local skills are listed for overlap awareness and never included in the stack.
- Requires explicit waiver phrase (e.g., “skip questions, assume defaults”) to proceed without answers.
- Context7 discovery requires the Context7 CLI (`ctx7`) or `npx -y ctx7`; if neither is available, the search log must mark Context7 as unavailable.
- skills.sh discovery must use the homepage leaderboard.
- skills.sh must also open at least one relevant skill detail page (or explicitly state none were relevant).
- Category focus is requested up front; users can pick any number or say “all.” Includes an **Other** option for custom categories.
- Verifies installs after confirmation (checks paths, reads SKILL.md, and summarizes installed skills).
- Requires a search matrix across selected categories × sources (Context7, skills.sh, GitHub) unless a source is unavailable.
- External candidates that match already-installed local skills are treated as already installed and excluded from recommendations.
- Searches skills registries and inspects candidates before recommending them.
- Prefers official or trusted sources and flags unproven skills as optional.
- States assumptions when the user explicitly waives questions.
- Recommends a minimal stack and installs only after confirmation.

## When to use
- "Find the best skills for this project"
- "Analyze this codebase and recommend a skill stack"

## Install

### Generic (any skills-enabled client)
- Place the entire `skill-hunter/` folder in the project-level skills directory for your client, or
- Import/upload the skill as a ZIP if your client uses a UI.

If you are unsure where your client expects skills, check its documentation for the project-level skills path or import flow.

### Claude Code (CLI)
Claude Code discovers skills from:
- **Personal (global)**: `~/.claude/skills/<skill-name>/`
- **Project-level**: `.claude/skills/<skill-name>/` (in the project root)
- Plugin skills: bundled with installed plugins

```bash
# Global install (available in all projects)
mkdir -p ~/.claude/skills
cp -R skill-hunter ~/.claude/skills/

# Or project-level install
mkdir -p .claude/skills
cp -R skill-hunter .claude/skills/
```

Note: `allowed-tools` frontmatter is supported only in Claude Code.

### Claude (Web/Desktop)
Upload the skill as a ZIP via Settings > Capabilities.
Requires Skills and Code Execution to be enabled (org admins may need to enable it first).

### Codex CLI
Project-level path under the repo root:
```bash
mkdir -p .codex/skills
cp -R skill-hunter .codex/skills/
```

Or use the skill installer if available:
```bash
python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo CE0Alex/skill-hunter --dest ./.codex/skills
```

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
