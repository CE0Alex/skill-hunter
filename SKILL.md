---
name: skill-hunter
description: Use when asked to analyze a project/codebase to recommend a skill stack, evaluate or de-duplicate skills, or install project-level skills based on repo context and user goals.
license: MIT
metadata:
  author: CE0Alex
  version: "1.0.2"
  short-description: Analyze a repo and recommend or install a best-fit skill stack.
  argument-hint: <repo-root|path|url>
---

# Skill Hunter

## Overview

Analyze the repo and user goals to assemble a minimal, justified skill stack. Prefer official sources, inspect every candidate, and install only after user confirmation using agent-specific locations.

## Inputs

- Project root or repo URL
- Target agent (Codex, Claude/Claude Code, or other)
- Goals and priority tasks
- Trust policy (official-only vs allow community)
- Constraints: network, tools, compliance, time
- Requires web access for registry searches

## Workflow

### 1) Build a project dossier
- Confirm project root; ask if unclear.
- Scan repo and subdirectories until the scope is unambiguous.
- Read key docs: `AGENTS.md`, `README*`, `docs/`, `CHANGELOG*`, `package.json`, `pyproject.toml`, `requirements*`, `go.mod`, `Cargo.toml`, `pom.xml`, `Makefile`, CI configs, infra/IaC files.
- Use `rg --files` and `rg -n` to find domain keywords, APIs, and workflows.
- Summarize: domain, stack, critical workflows, tools, constraints, and risks.

### 2) Ask clarifying questions
- Ask only what is needed to remove ambiguity: goals, priorities, timelines, environments, compliance, risk tolerance, and must-have workflows.
- If user intent is already clear, proceed without extra questions.

### 3) Discover candidate skills (evidence-based)
- Use `web.run` to search context7.com (skills tab) and skills.sh.
- Prefer official/trusted sources: skills created/maintained by the tool or company that owns the tech in the codebase.
- If a registry is unavailable, say so and fall back to GitHub search or the vendor's official docs.

### 4) Inspect each candidate (no assumptions)
Inspection checklist:
- Open SKILL.md and read frontmatter and body.
- Verify maintainer, license, and install method.
- Scan scripts/references for required tools and dependencies.
- Check activity signals (recent commits/releases, issues health).
- Confirm compatibility with the target agent.

### 5) Evaluate quality and overlap
- Rate trust tier: Official / Maintained / Community.
- Create a capability matrix to avoid duplicate coverage.
- If a skill is not well established, label it as optional and do not recommend it by default.

### 6) Recommend a stack (or variants)
- Provide a primary stack when there is a clear best choice.
- If not, provide 2-3 variants with tradeoffs (coverage vs risk vs maintenance).
- For each skill, include purpose, source, trust tier, and overlap notes.

### 7) Confirm and install (agent-aware)
- Ask the user to confirm the chosen stack before installing.

**Codex**
- Install to `<repo>/.codex/skills/<skill-name>` by default.
- If a skill is hosted on GitHub, use the installer with a project-level destination:
  - `python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py --repo owner/repo --path path/to/skill --dest ./.codex/skills`
  - Or: `--url https://github.com/owner/repo/tree/<ref>/path/to/skill`
- If not on GitHub, follow official install instructions and place the skill under `./.codex/skills/`.

**Claude / Claude Code**
- Claude uses uploaded skills (ZIP) via Settings > Capabilities.
- Package the skill folder as a ZIP and instruct the user to upload it; do not assume a repo-level path.

**Other clients**
- Ask for the official project-level skills path or CLI for that client.
- If no official guidance exists, present a best-effort option and mark it as unverified.

## Output format (concise)

- Project dossier: stack, goals, constraints, key workflows
- Candidate skills: source + trust tier + inspection notes
- Overlap analysis: what each skill covers and conflicts
- Recommendation: primary stack + optional variants
- Next step: confirm install target
