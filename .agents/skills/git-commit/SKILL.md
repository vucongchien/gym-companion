---
name: git-commit
description: 'Execute git commit with conventional commit message analysis and optional Gitmoji prepending.'
license: MIT
allowed-tools: Bash
---

# Git Commit (Conventional Commits + Gitmoji)

## Overview

Generate standardized, semantic git commits using the Conventional Commits specification.
If the commit message uses a Conventional Commit type, prepend the corresponding Gitmoji. Otherwise, Gitmojis are purely for reference.

## Commit Format

When a conventional commit type is present, format the message as:
```
<emoji> <type>(scope): <description>

[optional body]

[optional footer(s)]
```

### Examples:

- Single-line commit:
  `✨ feat(auth): add google login`
- Multi-line commit with body and footer:
  ```
  🐛 fix(db): resolve deadlock on transaction

  The database was experiencing deadlocks when concurrent transactions tried to update the user balance. Wrapping the update query in a row lock resolves this issue.

  Closes #42
  ```
- Reference commit (no conventional emoji matched, or emoji not used):
  `docs(readme): update installation steps`



## Conventional Commit Types and Gitmojis

Below is the mapping for conventional types. If one of these types is used, prepend the primary emoji:

| Type | Emoji | Description |
| :--- | :---: | :--- |
| `feat` | `✨` | New feature |
| `fix` | `🐛` | Bug fix |
| `docs` | `📝` | Documentation changes |
| `style` | `🎨` | Formatting, UI, style changes (no logic changes) |
| `refactor` | `♻️` | Code refactoring |
| `perf` | `⚡️` | Performance improvements |
| `test` | `✅` | Adding or updating tests |
| `build` | `📦️` | Build system or external dependencies |
| `ci` | `👷` | CI configuration and scripts |
| `chore` | `🔧` | General maintenance, chores, config changes |
| `revert` | `⏪️` | Reverting a previous commit |

### Specific Scopes/Use-cases (Optional but Recommended)

For more specific scenarios, use these combinations:

| Type | Emoji | Description |
| :--- | :---: | :--- |
| `chore(deps)` | `➕` / `➖` / `⬆️` | Add, remove, or upgrade dependencies |
| `fix(security)` | `🔒️` | Fix security issues / secrets management |
| `chore(db)` | `🗃️` | Database migrations / database related changes |
| `chore(release)` | `🔖` | Release / Version tags |
| `chore(wip)` | `🚧` | Work in progress |
| `style(ui)` | `💄` | UI layout, CSS, and aesthetic design changes |
| `refactor(cleanup)` | `🔥` | Remove dead code or files |
| `chore(locales)` | `🌐` | Internationalization / translation updates |



## Workflow

1. **Analyze changes**: Run `git diff` (or `git diff --staged`) and `git status --porcelain`.
2. **Draft the message**:
   - Determine the Conventional Commit `type` (e.g. `feat`, `fix`, `docs`).
   - If a type is identified, prepend the corresponding Gitmoji from the table above.
   - Use scope if it adds valuable context (e.g., `(db)`, `(auth)`).
   - Write a short, imperative description (e.g., `add google login`, NOT `added google login`).
3. **Execute commit**:
   - Stage files: `git add <files>`
   - Commit: `git commit -m "<emoji> <type>(scope): <description>"` (or without emoji/scope if not using conventional commit format).