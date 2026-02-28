---
name: creating-skills
description: Creates and edits Agent Skills (SKILL.md). Use when the user asks to create, write, edit, or improve a skill.
---

# Creating Skills

## Structure

```
.github/skills/skill-name/
├── SKILL.md           # Required. Directory name must match `name` field.
└── (optional files)   # Reference docs, scripts, examples
```

## SKILL.md format

```yaml
---
name: lowercase-hyphenated   # Max 64 chars. Letters, numbers, hyphens only.
description: Does X. Use when Y.  # Max 1024 chars. Third person. Specific.
# VS Code optional:
# argument-hint: "[input] [options]"
# user-invokable: true         # Show as /command
# disable-model-invocation: false  # Allow auto-loading
---
```

Body: Clear instructions, under 500 lines. Split to separate files if longer.

Write skills in English for best model performance and compatibility with the standard.

## Key principles

1. **Be concise** — Only add context the model doesn't already have.
2. **Description is critical** — Include WHAT it does AND WHEN to use it. Include trigger keywords.
3. **Progressive disclosure** — SKILL.md as overview; detail files loaded on-demand. Keep references one level deep.
4. **Match freedom to risk** — High freedom for flexible tasks, low for fragile operations.
5. **Consistent terminology** — Pick one term per concept throughout.
6. **No time-sensitive info** — Use "old patterns" sections instead.
7. **Forward slashes only** — Even on Windows.
8. **Workflows as checklists** — For complex multi-step tasks, include a copyable checklist:
   ```
   Copy this checklist and track your progress:
   - [ ] Step 1: ...
   - [ ] Step 2: ...
   ```
   This prevents the agent from skipping steps.
9. **Feedback loops** — Validate → fix → repeat for quality-critical tasks.
10. **Provide defaults** — Don't offer multiple options; give one good default with an escape hatch.
11. **Scripts over generation** — Pre-made utility scripts are more reliable. Handle errors explicitly, document constants.
