---
name: confirming-with-user
description: Defines when and how to use ask_questions to confirm with the user. Use when the agent needs to check with the user before proceeding, report autonomous decisions, or verify task completion.
---

# Confirming with the User via ask_questions

## When to Use ask_questions

### 1. Before or After Making an Autonomous Decision
Use `ask_questions` when the agent has made a judgment call on ambiguous requirements or chosen one approach over another without being explicitly told to do so.

### 2. When User Input is Required to Proceed
Use `ask_questions` when the task cannot proceed without additional information from the user (e.g., which file to overwrite, which approach to take).

### 3. After Task Completion
Always use `ask_questions` when the agent determines that the current task is fully complete, to ask if there is anything else the user wants to do.

---

## How to Use ask_questions

**Always follow this two-step pattern:**

### Step 1 — Markdown detail block (before invoking ask_questions)

Write a markdown section that explains:
- **What you did / what you are about to do** (context)
- **Each option in detail** — description, trade-offs, consequences

Example:

---
### Confirm

Implemented with the following approach. Will proceed unless you have concerns.

| Option | Description |
|--------|-------------|
| **Proceed** | Approve the current approach and move to the next step |
| **Redo** | Start over with a different approach |
| **Provide details** | Enter specific instructions to change the approach |

---

### Step 2 — ask_questions (summary version only)

After the markdown block, invoke `ask_questions` with **concise** labels — the markdown above already provides the full detail.

```
ask_questions({
  questions: [{
    header: "Confirm",
    question: "Please confirm the implementation approach",
    options: [
      { label: "Proceed", recommended: true },
      { label: "Redo" },
      { label: "Provide details" }
    ],
    allowFreeformInput: false
  }]
})
```

> **Key rule:** The `ask_questions` labels are short summaries. The full explanation lives in the markdown — never duplicate long text inside `ask_questions`.

---

## Task Completion Check

When you judge that the current task is **fully complete**, always confirm with the user using this pattern:

### Markdown block

---
### Task Complete

All requested work has been completed.

| Option | Description |
|--------|-------------|
| **Done** | Finish here |
| **Request more work** | Continue with another task |

---

### ask_questions (summary)

```
ask_questions({
  questions: [{
    header: "Task Done",
    question: "Is there anything else you'd like to do?",
    options: [
      { label: "Done", recommended: true },
      { label: "Request more work" }
    ],
    allowFreeformInput: true
  }]
})
```

---

## Rules Summary

| Situation | Action |
|-----------|--------|
| Agent made an autonomous decision | Show markdown detail → ask_questions (summary) |
| User input needed to proceed | Show markdown detail → ask_questions (summary) |
| Task fully complete | Show markdown detail → ask_questions (summary) |
| Simple info request (no decision required) | No ask_questions needed |

## Anti-Patterns

- ❌ Calling `ask_questions` without a preceding markdown explanation
- ❌ Putting long option descriptions inside `ask_questions` labels (keep labels short)
- ❌ Skipping the task-completion check after finishing a multi-step task
- ❌ Asking multiple unrelated questions in one batch unnecessarily
