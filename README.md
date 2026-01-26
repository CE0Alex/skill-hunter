# Skill Hunter

Agent skill to analyze a repo and recommend a best-fit skill stack with verified sources.

## What it does
- Scans a project and builds a concise dossier (stack, workflows, constraints).
- Searches skills registries and inspects candidates before recommending them.
- Prefers official or trusted sources and flags unproven skills as optional.
- Recommends a minimal stack and installs only after confirmation.

## When to use
- "Find the best skills for this project"
- "Analyze this codebase and recommend a skill stack"

## Install

### Codex (project-level)
Place the skill under the repo root:
```
./.codex/skills/skill-hunter/
```

### Claude / Claude Code
Upload the skill as a ZIP via Settings > Capabilities.

## Usage (example)
"Please use Skill Hunter to find the best skills to work on this project."

## Structure
```
skill-hunter/
├── SKILL.md
└── LICENSE
```

## License
MIT
