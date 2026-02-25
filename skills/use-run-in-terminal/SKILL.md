---
name: use-run-in-terminal
description: Defines the required workflow when calling run_in_terminal. Load when about to execute a terminal command.
---

# Use run_in_terminal Tool

When calling `run_in_terminal`:

1. Explain in plain text the command to be executed, including all flags and arguments, and what each does
2. Call `ask_questions` to invite the user to ask follow-up questions or confirm

Do not skip this step even for seemingly simple commands.
