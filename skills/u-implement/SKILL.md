---
name: u-implement
description: A structured workflow for planning and implementing features or fixes. Use when the user wants to implement something, add a feature, or make a change. Guides through four steps (requirements gathering → implementation plan → implementation → improvement suggestions), confirming with the user at each step before proceeding.
---

# u-implement Skill: Plan-then-Implement Workflow

This skill defines a structured workflow that clarifies requirements, presents an implementation plan for user review, and only then performs the actual implementation.

## Workflow

Track progress using a checklist. Display the checklist at the start of each step, marking completed steps with `[x]`. When returning to a previous step, uncheck all steps from that point onward.

```
### Workflow Progress
1. [ ] Requirements gathering
2. [ ] Implementation plan
3. [ ] Implementation
4. [ ] Improvement suggestions
```

---

## Step 1: Requirements Gathering

**Goal:** Collect all necessary information before creating an implementation plan.

**Procedure:**

1. Display the workflow progress checklist (all steps unchecked).
2. Use the **`ask_questions` tool** to ask the user about all unclear or uncertain aspects of the request in a single batch. Topics to consider:
   - Purpose and background of the implementation
   - Target files, components, or modules
   - Technical constraints and dependencies
   - Compatibility with existing code
   - Testing requirements
   - Performance requirements
3. Once all information is gathered, use the **`ask_questions` tool** to ask: "Ready to move on to Step 2 (Implementation Plan)?"
4. **Only proceed to Step 2 if the user explicitly confirms (e.g. "yes", "proceed", "go ahead").** Otherwise, restart from Step 1.

---

## Step 2: Implementation Plan

**Goal:** Present a detailed implementation plan, including only the changed code sections, based on the information gathered in Step 1.

**Procedure:**

1. Update and display the workflow progress checklist:
   ```
   ### Workflow Progress
   1. [x] Requirements gathering
   2. [ ] Implementation plan
   3. [ ] Implementation
   4. [ ] Improvement suggestions
   ```
2. Present the implementation plan in Markdown format, including:
   - **Overview:** Summary of what will be implemented
   - **Files to change:** List of files to be modified or created, with reasons
   - **Changed sections:** Only the relevant code snippets that will be added or modified, shown in code blocks (no diff notation, no full file — just the changed parts with enough surrounding context to locate them)
   - **Impact:** Effects on existing code
   - **Notes and risks:** Any caveats or potential issues
3. After presenting the plan, use the **`ask_questions` tool** to ask: "Ready to move on to Step 3 (Implementation)?"
4. **Only proceed to Step 3 if the user explicitly confirms.** Otherwise (e.g. the user requests changes), restart from Step 1.

---

## Step 3: Implementation

**Goal:** Implement the code based on the plan confirmed in Step 2.

**Procedure:**

1. Update and display the workflow progress checklist:
   ```
   ### Workflow Progress
   1. [x] Requirements gathering
   2. [x] Implementation plan
   3. [ ] Implementation
   4. [ ] Improvement suggestions
   ```
2. Execute the implementation plan:
   - Edit or create the necessary files.
   - After completing the implementation, report a summary of all modified files.
   - If any errors occur, fix them before moving to the next step.
3. After implementation is complete, use the **`ask_questions` tool** to ask: "Ready to move on to Step 4 (Improvement Suggestions)?"
4. **Only proceed to Step 4 if the user explicitly confirms.** Otherwise (e.g. the user requests fixes), restart from Step 1.

---

## Step 4: Improvement Suggestions

**Goal:** Reflect on the workflow and propose any improvements or opportunities to create new skills.

**Procedure:**

1. Update and display the workflow progress checklist:
   ```
   ### Workflow Progress
   1. [x] Requirements gathering
   2. [x] Implementation plan
   3. [x] Implementation
   4. [ ] Improvement suggestions
   ```
2. Review the entire workflow and compile suggestions from these angles:
   - Repetitive operations encountered during this workflow (candidates for new skills)
   - Reusable patterns for similar future implementations
   - Improvements to the `u-implement` skill itself
3. Use the **`ask_questions` tool** to present the suggestions and ask the user which, if any, to adopt.
4. If any suggestions are adopted, carry them out.
   - **If the suggestion involves creating or modifying any skill file** (not limited to `u-implement`), do NOT edit directly. Instead, restart the workflow from **Step 1** to plan and implement the change.
5. Use the **`ask_questions` tool** to ask: "Would you like to finish the workflow?"
6. **If the user confirms completion**, end the workflow. Otherwise (e.g. the user requests more changes or does not confirm), restart from **Step 1**.

---

## Important Rules

- **Always use the `ask_questions` tool** whenever asking the user a question (gathering requirements, step confirmations, suggestion reviews).
- **Never advance to the next step** without explicit user confirmation (e.g. "yes", "proceed", "go ahead").
- In the implementation plan (Step 2), show only the **changed code sections** with enough surrounding context to locate them — no full files, no diff notation.
- Always display the progress checklist at the beginning of each step.
- When returning to a previous step, uncheck all steps from that point onward before displaying the checklist.
- When presenting options via `ask_questions`, **show the full details of each option in the chat response (markdown) first**, then use `ask_questions` with short labels only (e.g. `①`, `②`). Do not put detailed descriptions inside the `description` field of `ask_questions` options.
