---
name: creating-skills
description: Provides best practices and rules to follow when creating or editing Agent Skills (SKILL.md files). Use when the user asks to create, edit, improve, or review a SKILL.md file or an Agent Skill directory.
---

# Creating and Editing Agent Skills

## Required Rules

### Directory Structure

```
.github/skills/
└── <skill-name>/        # Must match the name field exactly
    └── SKILL.md         # Required
    └── (optional supporting files)
```

Personal skills go in `~/.copilot/skills/`.

### YAML Frontmatter (required)

```yaml
---
name: skill-name          # Lowercase, numbers, hyphens only. Max 64 chars. Must match directory name.
description: ...          # What it does + when to use it. Max 1024 chars.
---
```

- `name`: no XML tags, no reserved words (`anthropic`, `claude`)
- `description`: no XML tags
- `description`: always write in **third person** — "Processes Excel files" ✅ / "I can help you" ❌

---

## Naming Conventions

- Prefer gerund form: `creating-skills`, `processing-pdfs`, `managing-databases`
- Noun phrases also acceptable: `pdf-processing`, `spreadsheet-analysis`
- Avoid vague names: `helper`, `utils`, `tools`, `documents`

---

## Writing Effective Descriptions

**Good:**
```
Processes Excel spreadsheets, creates pivot tables, generates charts.
Use when analyzing Excel files, spreadsheets, tabular data, or .xlsx files.
```

**Bad:**
```
Helps with documents
Does stuff with files
I can help you process Excel files
```

Include both **what it does** and **when to use it**. Copilot uses the description to decide which skill to load.

---

## SKILL.md Body Rules

1. **Be concise** — do not explain things Claude already knows; every token competes with context
2. **Stay under 500 lines** — split into separate files with progressive disclosure if needed
3. **Keep references one level deep** — SKILL.md → reference files only; no deeper nesting
4. **No time-sensitive information** — avoid "after August 2025, use..."; wrap legacy info in `<details>`
5. **Use consistent terminology** — pick one term per concept and stick to it
6. **Forward slashes only** — `scripts/helper.py` ✅ / `scripts\helper.py` ❌

---

## Progressive Disclosure Pattern

For larger skills, use supporting files loaded only when needed:

```
skill-name/
├── SKILL.md          # Overview and links (under 500 lines)
├── advanced.md       # Advanced features (loaded when needed)
├── reference.md      # API reference (loaded when needed)
└── scripts/
    └── helper.py     # Executable script
```

Example references in SKILL.md:
```markdown
**Basic usage**: [described below]
**Advanced features**: See [advanced.md](advanced.md)
**API reference**: See [reference.md](reference.md)
```

---

## Degree of Freedom

| Situation | Freedom | Approach |
|-----------|---------|----------|
| Multiple valid approaches | High | Text instructions only |
| A preferred pattern exists | Medium | Template + parameters |
| Order matters / fragile ops | Low | Exact commands / steps |

---

## Workflows and Feedback Loops

For complex multi-step tasks (5+ steps, destructive operations, or order-critical workflows), include a progress checklist and prompt the user to copy and track it:

```markdown
Copy this checklist and track your progress:

- [ ] Step 1: ...
- [ ] Step 2: ...
- [ ] Step 3: ...
```

> **When to include the checklist instruction:** Use it for complex or destructive workflows. Skip it for simple single-step skills — adding it unnecessarily inflates the skill.

For quality-critical tasks, implement a feedback loop:
1. Execute
2. Validate
3. If errors found, fix and return to step 2
4. Proceed only when validation passes

---

## Anti-Patterns to Avoid

- ❌ Too many options (provide one default with an escape hatch)
- ❌ Windows-style paths (backslashes)
- ❌ Deeply nested references (SKILL.md → A.md → B.md → ...)
- ❌ Long reference files without a table of contents (add TOC for files over 100 lines)
- ❌ Unexplained magic numbers (document the reason in a comment)

---

## Checklist for Effective Skills

### Core quality
- [ ] `description` is specific and includes both what it does and when to use it
- [ ] SKILL.md body is under 500 lines
- [ ] No time-sensitive information
- [ ] Terminology is consistent throughout
- [ ] File references are one level deep only

### Structure
- [ ] Directory name matches the `name` field
- [ ] All paths use forward slashes
- [ ] Reference files over 100 lines have a table of contents

### Testing
- [ ] Tested with real usage scenarios
- [ ] Skill activates automatically as expected

---

## Optional Frontmatter Fields

| Field | Description |
|-------|-------------|
| `argument-hint` | Hint text shown when skill is invoked as a slash command |
| `user-invokable: false` | Hide from `/` menu; allow automatic trigger only |
| `disable-model-invocation: true` | Disable automatic trigger; manual invocation only |
