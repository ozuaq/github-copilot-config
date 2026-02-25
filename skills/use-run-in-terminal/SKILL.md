---
name: use-run-in-terminal
description: ALWAYS load before calling run_in_terminal. Defines mandatory steps: explain the command to be executed, then call ask_questions.
---

# Use run_in_terminal Tool

When calling `run_in_terminal`:

1. Explain in plain text the command to be executed, including all flags and arguments, and what each does
2. Call `ask_questions` to invite the user to ask follow-up questions or confirm

Do not skip this step even for seemingly simple commands.
