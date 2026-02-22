# Commit Message Template

Use this format when the human asks for a commit message.

## Format

```text
<type>: <summary>

- <outcome 1>
- <outcome 2>
- <outcome 3>
  - <optional grouped detail>
  - <optional grouped detail>
```

Rules:
- Use a Conventional Commit type (`feat`, `fix`, `chore`, `docs`, `refactor`, `test`, `build`, `ci`).
- Keep the subject line specific and scoped to the checkpoint/thread.
- Use flat bullets for main outcomes.
- Use indented sub-bullets only when grouping related artifacts/tooling.
- Keep body focused on what changed and why (no filler).

## Copy/paste request for thread end

```text
Generate commit message using `/docs/templates/COMMIT_MESSAGE_TEMPLATE.md` and this thread context.
```
