# Instructions for Writing Code

## Core Philosophy
1. Implement only what delivers user-visible value; remove anything superfluous (**Minimalism First**).
2. Write code that reads like prose and is desirable to include in any codebase (**Clarity and Cleverness**).
3. Avoid multiple abstractions doing the same job; choose one clear way to do it (**One Way to Do It**).

---

## Universal Guidelines
1. Do not use CLI arguments. Accept configuration via function parameters, `.env`, or a minimal config file. Never use `sys.argv`, `argparse`, or shell flags.
2. Prefer the standard library or native browser APIs. Justify each extra package in code comments. Keep dependencies to zero or a minimum.
3. Keep repository structures flat (no more than one nested folder level). Use single-file scripts when feasible.
4. Write pure functions by default. Use classes only when persistent state or polymorphism is essential.
5. Auto-format code: use Black for Python and Prettier for JS/TS, with a 100-character line limit.
6. Use well-named variables instead of comments. Add docstrings or JSDoc only for public APIs.
7. Unit-test core logic with pytest (Python) or vitest (JS). Avoid heavy plugins or complex fixtures.
8. Isolate environments: use **uv** (Python) and bare `npm` (JS) for lightweight, hermetic installs. Avoid Conda, Docker, or global installs unless absolutely required.
9. Ensure determinism: seed random number generators and avoid time, network, or filesystem side-effects inside pure logic layers.

---

## Python-Specific Instructions
1. Do not use external modules unless they are mission-critical and unavailable in the standard library.
2. Use type hints for all public-facing functions.
3. Prefer dataclasses over ad-hoc dicts for structured data.

## JavaScript / TypeScript / Next.js Instructions
1. Use ESM only; do not use CommonJS `require`.
2. Co-locate Tailwind styles with components.
3. Keep component trees shallow. Extract smaller presentational components before adding hooks.


# Minimal Coding Instructions

## General Principles

### 1. KISS (Keep It Simple, Stupid)
- Always choose the simplest solution that works.
- Do not add unnecessary complexity.
- Avoid clever hacks or one-liners that obscure meaning.
- Do not optimize prematurely unless there is a clear benefit.

### 2. YAGNI (You Aren’t Gonna Need It)
- Implement only what is required for current requirements and user stories.
- Do not add features or code for speculative future needs.
- Only include libraries or components when absolutely necessary.

### 3. DRY (Don’t Repeat Yourself)
- Refactor or abstract common logic so it exists in only one place.
- Reuse functions or modules for repeated functionality.
- Do not duplicate code across functions or modules.
- Avoid copy-pasting; extract shared helpers or constants instead.

### 4. Be Explicit, Not Implicit
- Write code that clearly shows its intent.
- Use clear variable names and straightforward control flow.
- Use keyword arguments or named constants to make code self-documenting.
- Do not rely on implicit behaviors or side effects.
- Avoid magic numbers or strings; use named constants.

### 5. Use Small, Composable Units
- Encapsulate functionality in small functions, each doing one task.
- Keep functions ≤ 20-30 lines of code.
- Keep cyclomatic complexity ≤ 10; refactor if it grows beyond this.
- Limit function parameters (max 5); group data in objects or dictionaries if needed.
- Organize code into focused modules/files; prefer more small files over one large file.
- Do not write large, multi-purpose functions; break them into helpers.
- Avoid deeply nested loops or conditionals; split into smaller functions if nesting exceeds 2-3 levels.
- Do not put unrelated code in the same file.

## Language-Specific Instructions

### Python
- Follow PEP 8 style guidelines; use a formatter like Black.
- Prefer standard library or simple built-ins over external dependencies.
- Use simple, readable loops or comprehensions (avoid nested comprehensions beyond 2 levels).
- Use docstrings and comments to explain non-obvious code.
- Do not use wildcard imports (e.g. `from module import *`).
- Avoid unnecessary classes or inheritance; use simple functions or data structures when possible.
- Remove unused variables or dead code.
- Avoid heavy metaprogramming or magic tricks; prefer straightforward implementations.
- Use these tools:
  - **Formatter:** Black
  - **Linter:** Ruff
  - **Type Checker:** Mypy (optional)
  - **Complexity Checker:** Radon

### JavaScript
- Use modern ES6+ syntax (`const`/`let`, arrow functions).
- Keep functions pure and side-effect-free when possible.
- Use array methods (`.map`, `.filter`, etc.) for simple transformations; use basic loops if logic is complex.
- Encapsulate code in modules or closures; avoid polluting the global namespace.
- Use comments or JSDoc to explain complex logic or important decisions.
- Do not define new global variables; use local or module scope.
- Avoid long chains of method calls or callbacks; use intermediate variables or async/await for clarity.
- Do not add large dependencies for trivial tasks; prefer built-in or lightweight helpers.
- Do not use `eval` or similar dynamic code execution.
- Use these tools:
  - **Formatter:** Prettier
  - **Linter:** ESLint (minimal config)
  - **Complexity Checker:** ESLint complexity rule (max complexity = 10)
  - **Type Checker:** TypeScript (optional)

## Tooling and Automation
- Use formatters and linters to enforce style and catch issues automatically.
- Use type checkers and complexity checkers to maintain explicitness and simplicity.
- Run these tools in CI to enforce rules and keep the codebase minimal and maintainable.
