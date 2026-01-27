# AGENTS.md

Guidance for agents working on the **skill-hunter** repo.

## Project Overview
Skill Hunter is a meta-skill that discovers **new external skills** for a project, evaluates them, and installs only after user confirmation.

## Key Files
- `SKILL.md` – core workflow and rules (keep lean; link to references for details)
- `README.md` – user-facing docs and install instructions
- `references/installation.md` – per-agent install guidance (load only after confirmation)

## Common Commands
```bash
# Package the skill (avoid including .git or dist)
python3 ~/.codex/skills/.system/skill-creator/scripts/package_skill.py /path/to/skill-hunter /path/to/dist

# Sync global installs (Codex + Claude Code)
cp -R /path/to/skill-hunter ~/.codex/skills/skill-hunter
cp -R /path/to/skill-hunter ~/.claude/skills/skill-hunter
```

## Change Guidelines
- Keep **SKILL.md** focused on discovery and decision rules; move heavy install details to `references/installation.md`.
- Preserve “external-only recommendations” and search-matrix requirements.
- Always update `README.md` when modifying workflow or install guidance.
- Do **not** hardcode usernames, personal paths, or private repo names in docs or examples; use placeholders like `owner/repo` and `<repo>/`.
- For Codex install guidance, use the built-in `$skill-installer` (do not reference internal Python scripts).

## Quick Verification
- Confirm `SKILL.md` still uses only `name` and `description` in YAML frontmatter.
- Ensure new references are linked from `SKILL.md` (progressive disclosure).
