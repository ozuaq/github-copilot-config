---
name: use-ask-questions
description: Defines when and how to use the ask_questions tool. Load when about to ask the user a question, seek confirmation, after editing files, when all tasks are complete, or when calling run_in_terminal.
---

# Use ask_questions Tool

Always use the `ask_questions` tool (never plain chat text) in these situations:

1. **Before acting** on ambiguous or unclear requests
2. **When presenting choices** to the user
3. **After editing files** – confirm the result with the user
4. **When all tasks are complete** – ask if there is anything else to do
5. **When calling `run_in_terminal`** – explain the command (all flags and arguments, and what each does) before running, then call `ask_questions`

## When questions or choices are complex

Before invoking `ask_questions`, first explain in plain text:
- The details of the question
- Each choice with its label and full description

Then call `ask_questions` with labels only (no description in options).

Do not ask via plain text when the `ask_questions` tool is available.
