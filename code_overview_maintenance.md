# `code_overview.md` Maintenance Mandate

**Before completing any task that modifies the codebase, you MUST update `.clinerules/code_overview.md` if your changes involve any of the following:**

1. **Adding or Removing Files**: Any new files added to, or existing files removed from, the directory.
2. **Significant Refactoring**: Changes to functions or classes within any file that alter their:
   * Core purpose.
   * Key components or data structures.
   * Primary internal or external dependencies.
3. **Altered Interdependencies**: Modifications to how different modules within `codebase` interact with each other (e.g., new import paths, changed function call signatures between modules).

**Failure to update `.clinerules/code_overview.md` as required will result in an incomplete task.**