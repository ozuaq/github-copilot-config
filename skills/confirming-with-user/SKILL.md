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
### 確認

以下の方針で実装しました。問題なければそのまま続けます。

| 選択肢 | 内容 |
|--------|------|
| **このまま続ける** | 現在の実装方針を承認し、次のステップへ進みます |
| **やり直す** | 別のアプローチで最初からやり直します |
| **詳細を教える** | 方針を変更する具体的な指示を入力してください |

---

### Step 2 — ask_questions (summary version only)

After the markdown block, invoke `ask_questions` with **concise** labels — the markdown above already provides the full detail.

```
ask_questions({
  questions: [{
    header: "方針確認",
    question: "実装方針を確認してください",
    options: [
      { label: "このまま続ける", recommended: true },
      { label: "やり直す" },
      { label: "詳細を教える" }
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
### タスク完了

依頼された作業がすべて完了しました。

| 選択肢 | 内容 |
|--------|------|
| **完了** | 作業をここで終了します |
| **追加作業を依頼する** | 続けて別の作業を指示できます |

---

### ask_questions (summary)

```
ask_questions({
  questions: [{
    header: "タスク完了",
    question: "他にやることはありますか？",
    options: [
      { label: "完了", recommended: true },
      { label: "追加作業を依頼する" }
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
