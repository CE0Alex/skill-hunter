---
name: skill-hunter
description: Use when asked to analyze a project/codebase to recommend a skill stack, evaluate or de-duplicate skills, or install project-level skills based on repo context and user goals.
---

# Skill Hunter

## Overview

Analyze the repo and user goals to assemble a minimal, justified skill stack. Prefer official sources, inspect every candidate, and install only after user confirmation.

## Required inputs (confirm before external search)

- Goals and priority tasks
- Trust policy / tiers to target (official-only vs allow maintained vs allow community)
- Permission to browse external sources (ask only if not already granted in this session)

If any required input is missing, ask for it and stop. Do not list candidates or recommendations until the user answers or explicitly waives questions.

## Workflow

### 1) Build a project dossier
- Confirm project root; ask if unclear.
- Scan repo and subdirectories until the scope is unambiguous.
- Read key docs: `AGENTS.md`, `README*`, `docs/`, `CHANGELOG*`, `package.json`, `pyproject.toml`, `requirements*`, `go.mod`, `Cargo.toml`, `pom.xml`, `Makefile`, CI configs, infra/IaC files.
- Find domain keywords, APIs, and workflows using your agent's file discovery and content search tools.
- Summarize: domain, stack, critical workflows, tools, constraints, and risks.

### 2) Ask clarifying questions (required)
- Ask clarifying questions **before any external search**.
- Do not ask which agent is in use; assume the current client.
- Proceed to Step 3 only after answers **or** an explicit user waiver such as “skip questions, assume defaults.”
- If the user waives questions, record the assumptions and state them in your response.
- Ask for permission to browse only if not already granted.
- Ask which trust tiers to target (official-only, maintained, community) if not provided.
- Do not present candidate lists or recommendations in this step.

### 3) Discover candidate skills (evidence-based)
- Do not browse until required inputs are confirmed.
- If browsing permission is denied, skip external search and limit discovery to local skills; state the limitation clearly.
- Search skill registries and sources using your agent's web search/browse tools.

Search targets:
- context7.com (skills tab)
- skills.sh
- GitHub search: `SKILL.md in:path <technology>`

Prefer official/trusted sources: skills created/maintained by the tool or company that owns the tech in the codebase. If a registry is unavailable, say so and fall back to GitHub search or the vendor's official docs.

### 4) Inspect each candidate (no assumptions)
Inspection checklist:
- Open SKILL.md and read frontmatter and body.
- Verify maintainer, license, and install method.
- Scan scripts/references for required tools and dependencies.
- Check activity signals (recent commits/releases, issues health).
- Confirm compatibility with the target agent (current client).

### 5) Evaluate quality and overlap
- Rate trust tier: Official / Maintained / Community.
- Create a capability matrix to avoid duplicate coverage.
- If a skill is not well established, label it as optional and do not recommend it by default.

### 6) Recommend a stack (or variants)
- Provide a recommended stack only after required inputs are confirmed (or explicitly waived) and discovery/inspection is complete.
- If there is no clear single best choice, provide 2-3 variants with tradeoffs (coverage vs risk vs maintenance).
- For each skill, include purpose, source, trust tier, and overlap notes.

### 7) Confirm and install (agent-aware)
- Only install after the user confirms their chosen stack.

**Codex CLI**
- Install to `<repo>/.codex/skills/<skill-name>/` by default.
- If a skill is hosted on GitHub, use the installer with a project-level destination:
  - `python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py --repo owner/repo --path path/to/skill --dest ./.codex/skills`
  - Or: `--url https://github.com/owner/repo/tree/<ref>/path/to/skill`
- If not on GitHub, use your shell tool to clone/download and place the skill under `./.codex/skills/`.

**Claude Code (CLI)**
- Project-level: `<repo>/.claude/skills/<skill-name>/`
- Personal (global): `~/.claude/skills/<skill-name>/`
- Use your shell tool to clone repos or download files, then place the skill folder in the appropriate directory.
- No ZIP packaging needed for CLI usage.

**Claude (Web/Desktop)**
- Package the skill folder as a ZIP.
- Upload via Settings > Capabilities (requires Skills and Code Execution enabled).

**Other clients**
- Ask for the official project-level skills path or CLI for that client.
- If no official guidance exists, present a best-effort option and mark it as unverified.

## Assumptions (only if user waives questions)

If the user explicitly waives questions, state the assumptions in your response. Defaults:
- Goals: recommend the best-fit skill stack for the project
- Trust policy: official-only
- Permission to browse: use existing permission; if none, ask before browsing
- Project root: current working directory

## Output format (concise)

If required inputs are missing: ask questions only and stop.

- Project dossier: stack, goals, constraints, key workflows
- Candidate skills: source + trust tier + inspection notes
- Overlap analysis: what each skill covers and conflicts
- Recommendations: primary stack + optional variants
- Assumptions (if any)
- Next step: confirm install target
