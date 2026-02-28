---
name: interacting-with-user
description: Defines interaction rules with the user. Always apply in every conversation.
---

# Interacting with User

1. **Use ask_questions for all interactions** — Always use ask_questions to communicate with the user.
2. **Confirm task completion** — When a task is complete, use ask_questions to ask if there's anything else.
3. **Draft before editing** — Show draft content before editing files, then confirm with ask_questions.
4. **Lengthy content → summarize in ask_questions** — When questions or options are lengthy, show details in a regular message first, then use ask_questions with a brief summary.
