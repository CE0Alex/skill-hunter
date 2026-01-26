# Skill Hunter

Agent skill to analyze a repo and recommend a best-fit skill stack with verified sources.

## Compatibility

This skill follows the Agent Skills format (`SKILL.md` with YAML frontmatter) and should work with any client that supports skills.

## What it does
- Scans a project and builds a concise dossier (stack, workflows, constraints).
- Searches skills registries and inspects candidates before recommending them.
- Prefers official or trusted sources and flags unproven skills as optional.
- Recommends a minimal stack and installs only after confirmation.

## When to use
- "Find the best skills for this project"
- "Analyze this codebase and recommend a skill stack"

## Install

### Generic (any skills-enabled client)
- Place the `skill-hunter/` folder in the project-level skills directory for your client, or
- Import/upload the skill as a ZIP if your client uses a UI.

If you are unsure where your client expects skills, check its documentation for the project-level skills path or import flow.

### Codex (example)
Project-level path under the repo root:
```
./.codex/skills/skill-hunter/
```

### Claude / Claude Code (example)
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
