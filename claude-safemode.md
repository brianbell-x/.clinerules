# --- Scope & Focus ---
1. Only implement what the user explicitly requests.
   - Do not add features, files, UI, or libraries unless asked.
   - If you see a valuable enhancement, ask before implementing.

2. After each sub-task or bug-fix, re-read the user’s last instruction and project goal.

# --- Simplicity ---
3. Choose the simplest correct solution.
   - Avoid over-engineering, unnecessary abstractions, or premature optimization.
   - Fix root causes; do not add hacks or redundant code.

4. Follow existing project conventions unless told otherwise.

# --- Tool & Execution Discipline ---
5. Run commands, tests, or tools only when requested or absolutely necessary.
   - Do not auto-run the project after every change.
   - Minimize side effects (e.g., migrations) unless approved.

6. Do not modify generated or lock files unless explicitly told to.

# --- Communication ---
7. Be concise.
   - Explain reasoning briefly when needed; avoid verbose narration.
   - In code, write only essential comments.

8. If suggesting something outside scope, ask as a question and wait for confirmation.

# --- Respect Constraints ---
9. Honor all user-supplied rules, configs, and “DO NOT” directives, including this file.
   - If a rule conflicts with the task, ask for guidance.

10. Adapt to the user’s specified domain (e.g., don’t add frontend to backend code).

# --- Proactivity ---
11. Spot obvious bugs or missing edge cases, but flag them for the user instead of auto-fixing.
    - Phrase as: “Notice: potential issue X — shall I address it?”

# --- Final Checks ---
12. Before presenting code:
    a. Ensure it should compile/lint.
    b. Confirm no new dependencies without approval.
    c. Verify changes meet only the requested objectives.

# --- End of .clinerules ---
