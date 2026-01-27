# Skill Hunter

Agent skill to analyze a repo and recommend a best-fit **external** skill stack with verified sources.

## Compatibility

This skill follows the Agent Skills format (`SKILL.md` with YAML frontmatter) and is designed to work across multiple AI coding agents that support skills.

### Tested agents
| Agent | Version tested | Status |
|-------|----------------|--------|
| Claude Code (CLI) | 2.1.19 | ✅ Supported |
| Codex CLI | 0.91.0 | ✅ Supported |
| Claude (Web/Desktop) | — | ✅ Supported (ZIP upload) |

### Supported agents (via Skills CLI registry)
Skill Hunter does not hardcode a supported‑agent list to avoid drift. The canonical list is maintained by the Skills CLI registry. If an agent isn’t in the registry, installation support is unverified.

Reference: https://github.com/vercel-labs/skills (agents registry in `src/agents.ts`)

> Last verified: 2026-01-27
>
> Installation method verification based on:
> - [OpenAI Codex Skills Documentation](https://developers.openai.com/codex/skills/)
> - [OpenAI Skills GitHub Repository](https://github.com/openai/skills) (Codex CLI v0.91.0)
> - [Claude Code Skills Documentation](https://code.claude.com/docs/en/skills) (Claude Code CLI v2.1.19)

## What it does
- Scans a project and builds a concise dossier (stack, workflows, constraints).
- Asks clarifying questions and trust tier preferences before any external search.
- Does **not** ask about browsing if the client already has browsing enabled; only asks if browsing is explicitly disabled/denied.
- If required inputs are missing, asks questions only and does not present candidates or recommendations.
- When external browsing is permitted and available, requires a concise search log and inspection notes before recommendations.
- Uses `npx skills find <query>` as the preferred skills.sh discovery path (falls back to skills.sh web only if CLI is unavailable).
- Prioritizes Context7 + skills.sh registries; GitHub search is secondary but still used to catch high‑value gaps.
- Recommendations are based on **external skills only**; local skills are listed for overlap awareness and never included in the stack.
- If the user only wants guidance on already-installed/local skills, Skill Hunter should not run.
- Recommendations include a confidence rating (High/Medium/Low) with a brief rationale; Low-confidence skills are listed separately as Experimental/Unverified.
- Requires explicit waiver phrase (e.g., “skip questions, assume defaults”) to proceed without answers.
- Context7 discovery requires the Context7 CLI (`ctx7`) or `npx -y ctx7`; if neither is available, the search log must mark Context7 as unavailable.
- skills.sh discovery can use `npx skills find <query>` (preferred) or the homepage leaderboard.
- skills.sh must also open at least one relevant skill detail page (or explicitly state none were relevant).
- Category focus is requested up front; users can pick any number or say “all.” Includes an **Other** option for custom categories.
- Clarifying questions use **multi‑select choices** with an **Other** free‑text option and allow “use defaults.”
- Verifies installs after confirmation (checks paths, reads SKILL.md, and summarizes installed skills).
- Requires a search matrix across selected categories × sources (Context7, skills.sh, GitHub) unless a source is unavailable.
- External candidates that match already-installed local skills are treated as already installed and excluded from recommendations.
- Searches skills registries and inspects candidates before recommending them.
- Prefers official or trusted sources and flags unproven skills as optional.
- States assumptions when the user explicitly waives questions.
- Recommends a minimal stack and installs only after confirmation.
- Notes required installs/dependencies and any security/data‑access risks per recommended skill.
- Requires a **per-skill install method** verified during inspection; does not default to `npx skills add` unless the skill is from Skills CLI discovery.
- If a skill lacks a verified install method, it is marked unverified and not installed.
- If manual copying is required, it uses the verified source and the agent-specific paths in `references/agent-skills.md` (no reconstruction).
- Requires each candidate’s `SKILL.md` to be opened from the source; if not possible, the candidate is marked unverified and excluded from primary recommendations.

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
- **Project-level** (recommended): `.claude/skills/<skill-name>/` (in the project root)
- **Personal (global)**: `~/.claude/skills/<skill-name>/`
- Plugin skills: bundled with installed plugins

```bash
# Project-level install (recommended)
mkdir -p .claude/skills
cp -R skill-hunter .claude/skills/

# Or global install (available in all projects)
mkdir -p ~/.claude/skills
cp -R skill-hunter ~/.claude/skills/
```

Or install directly from GitHub:
```bash
# Project-level from GitHub
mkdir -p .claude/skills && git clone https://github.com/owner/repo-name.git .claude/skills/skill-name

# Global from GitHub
mkdir -p ~/.claude/skills && git clone https://github.com/owner/repo-name.git ~/.claude/skills/skill-name
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

Or use the built-in `$skill-installer` skill within Codex:
```
$skill-installer install https://github.com/owner/repo-name/tree/main/skill-name
```

You can also describe what to install:
```
$skill-installer install the skill-hunter skill from owner/repo-name
```

> **Note:** Restart Codex after installing new skills to register them.

## Repo Structure
```
skill-hunter/
├── SKILL.md                 # Core workflow + rules
├── README.md                # This file
├── AGENTS.md                # Contributor/agent workflow guide
├── references/installation.md  # Install guidance (load only after user confirms)
├── references/agent-skills.md   # Agent paths + skill format + discovery locations
└── LICENSE
```

## Usage (example)
"Please use Skill Hunter to find the best skills to work on this project."

## Structure
```
skill-hunter/
├── SKILL.md      # The skill definition
├── README.md     # This file
├── references/agent-skills.md   # Agent paths + skill format + discovery locations
└── LICENSE       # MIT license
```

## License
MIT
