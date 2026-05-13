---
name: skillhub-cli-workflow
description: Manages project-local skills with skillhub CLI. Use when user asks to search, install, list, or upgrade skills in the current repository.
---

# Skillhub CLI Workflow

## Scope

Use this skill for managing project skills under `.cursor/skills` in this repository.

## Defaults

- Prefer project-local install target: `.cursor/skills`.
- Use explicit binary path when needed: `~/.local/bin/skillhub`.
- Report clear next action if remote search is unavailable.

## Standard Commands

1. Search:
   - `~/.local/bin/skillhub search <keyword>`
2. Install to project:
   - `~/.local/bin/skillhub --dir .cursor/skills install <skill-slug>`
3. List installed:
   - `ls .cursor/skills`
4. Upgrade installed:
   - `~/.local/bin/skillhub --dir .cursor/skills upgrade`

## Validation

After install/upgrade:

1. Verify directory exists: `.cursor/skills/<skill-slug>`
2. Verify `SKILL.md` exists in installed skill folder.
3. Return total count of project skills on request.
