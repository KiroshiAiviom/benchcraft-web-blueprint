# AGENTS hierarchy (how Codex loads instructions)

Codex can load instructions from multiple locations so rules can stay small and scoped.

## Project-level loading (root → leaf)

Within a project, Codex walks from the project root to the current directory. In each directory it loads **at most one** instruction file:

1) `AGENTS.override.md` (if present)
2) otherwise `AGENTS.md`

This enables folder-specific rules without keeping everything in a single large file.

## When to use `AGENTS.override.md`

Use an override when you need a deliberate, scoped rule swap, for example:

- stricter rules for a specific subsystem (e.g., security-sensitive code),
- different conventions in a generated code folder,
- temporary local hardening (often kept uncommitted).

Prefer `AGENTS.md` for normal, additive rules.

