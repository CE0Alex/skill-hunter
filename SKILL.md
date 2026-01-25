---
name: skill-hunter
description: Use when asked to analyze a project/codebase to recommend a skill stack, search skill registries (context7.com skills, skills.sh), compare or de-duplicate skills, or install project-level skills based on repo context and user goals.
---

# Skill Hunter

## Overview

Analyze the project and user goals to build a justified, minimal skill stack. Prefer official/trusted sources, verify each candidate by inspection, and install only after user confirmation using agent-specific locations.

## Workflow

### 1) Build a project dossier
- Confirm project root; ask if unclear.
- Scan repo and subdirectories until the scope is unambiguous.
- Read key docs: `AGENTS.md`, `README*`, `docs/`, `CHANGELOG*`, `package.json`, `pyproject.toml`, `requirements*`, `go.mod`, `Cargo.toml`, `pom.xml`, `Makefile`, CI configs, infra/IaC files.
- Use `rg --files` and `rg -n` to find domain keywords, APIs, and workflows.
- Summarize: domain, stack, critical workflows, tools, constraints, and risks.

### 2) Ask clarifying questions
- Ask only what’s needed to remove ambiguity: goals, priorities, timelines, environments, compliance, risk tolerance, and “must-have” workflows.
- If user intent is already clear, proceed without extra questions.

### 3) Discover candidate skills (evidence-based)
- Use `web.run` to search **context7.com (skills tab)** and **skills.sh**.
- Prefer official/trusted sources: skills created/maintained by the tool or company that owns the tech in the codebase.
- For each candidate, **inspect the skill contents** (open `SKILL.md` or official docs). Do not assume based on name alone.

### 4) Evaluate quality and overlap
- Note maintenance signals: recent activity, releases, issue health, community adoption.
- If a skill is not well established, **call that out clearly** and offer it only as an optional, non-recommended candidate.
- Map capabilities to project needs; avoid overlapping or redundant skills unless explicitly required.

### 5) Propose a stack (or variants)
- Present a **primary stack** when there is a clear best choice.
- If not, present 2–3 **stack variations** with tradeoffs (coverage vs. risk vs. maintenance).
- For each skill, include: purpose, source, trust level, and overlap notes.

### 6) Confirm agent + install (agent-aware)
- Ask the user to confirm the chosen stack **before installing**.
- Determine the target agent (Codex, Claude/Claude Code, or other). If unclear, ask.

**Codex**
- Install to `<repo>/.codex/skills/<skill-name>` by default.
- If user wants a narrower scope, install to `.codex/skills` in the current folder or a parent folder.
- If a skill is hosted on GitHub, use the installer with a project-level destination:
  - `python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py --repo owner/repo --path path/to/skill --dest ./.codex/skills`
  - Or: `--url https://github.com/owner/repo/tree/<ref>/path/to/skill`
- If not on GitHub, follow official install instructions and place the skill folder under `./.codex/skills/<skill-name>`.

**Claude / Claude Code**
- Claude uses uploaded skills (ZIP) via Settings > Capabilities.
- Package the skill folder as a ZIP and instruct the user to upload it; do not assume a repo-level path.

**Other clients**
- Ask for the official project-level skills path or CLI for that client.
- If docs exist, follow their official install method; otherwise, present a best-effort option and mark it as unverified.

## Output format (concise)
- **Project dossier:** stack, goals, constraints, key workflows
- **Candidate skills:** source + trust level + inspection notes
- **Overlap analysis:** what each skill covers and conflicts
- **Recommendation:** primary stack + optional variants
- **Next step:** confirm to install into `./skills`
