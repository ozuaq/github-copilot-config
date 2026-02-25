---
name: create-skill
description: Guide for creating a new agent skill (SKILL.md). Use when asked to create or set up a new skill.
---

# Create Agent Skill

## Structure

Place `SKILL.md` in `.github/skills/<skill-name>/`. Directory name must match `name` field.

```md
---
name: <skill-name>
description: <when and what this skill does>
---

# Instructions
```

## Rules for all skills

- Natural language: English only
- Total lines: 30 or fewer (including frontmatter)
- Omit anything the agent can infer; only include non-obvious, skill-specific instructions

## Optional frontmatter

- `argument-hint`: hint text shown in chat input
- `user-invokable: false`: auto-load only, not shown in `/` menu
- `disable-model-invocation: true`: manual invocation only
