# Setup (macOS)

This document describes the **minimum, repeatable** setup to use the Benchcraft Web workflow on macOS.

The goal is a stable baseline; see `docs/STACK_BASELINE.md` for the canonical stack/workflow baseline.


---

## 1) Required tools

Required:

- **Homebrew** (system package manager)
- **mise** (recommended) to pin tool versions per-machine and per-project
- **Node.js** (LTS/current) + **Bun**
- **Git**
- **Codex App** (primary surface)

Recommended:

- **VS Code** (for manual inspection and surgical edits)
- **GitHub CLI (`gh`)** (PR workflow)

Optional:

- **OrbStack** (or Docker Desktop) for local containers (Postgres, Redis, etc.)

---

## 2) Install checklist

### Homebrew

Install Homebrew from the official site and confirm:

```bash
brew --version
```

### mise

Install `mise`, then enable it in your shell (per mise docs). Confirm:

```bash
mise --version
mise current
```

### Node + Bun

Install Node and Bun via `mise` (example commands):

```bash
mise use -g node@lts
mise use -g bun@latest
```

Confirm:

```bash
node -v
bun --version
```

### Git

Confirm:

```bash
git --version
```

### Codex App

Install the Codex App from OpenAI, sign in, then:

- Configure at least one **Local Environment** that can run `bun`, `node`, and `git`.
- Ensure **web search** is enabled (cached is fine for most work).
- Use **worktrees** for parallel lanes (Builder / Review / Tests) and for any non-trivial change.
- Set the model to **GPT-5.3-Codex** and default reasoning effort to **medium** (use **high** / **xhigh** only when needed).
- (Optional) Enable steering while Codex works: Settings → General → Follow-up behavior.

> Keep one thread per checkpoint to avoid context drift.

### VS Code (recommended)

Install VS Code and these baseline extensions:

- Codex extension (optional, for IDE-side edits)
- Biome
- Tailwind CSS IntelliSense

### Containers (optional)

If you expect Postgres and other services locally, install OrbStack (or Docker Desktop).
Confirm:

```bash
docker --version
docker compose version
```

---

## 3) Health check (quick)

Run this to confirm your PATH and core tools:

```bash
which brew mise node bun git
brew --version
mise current
node -v
bun --version
git --version
```

Optional checks:

```bash
which gh docker
gh --version
docker --version
docker compose version
```

---

## 4) Bootstrap a new web project (Next.js + Bun)

Create a clean Next.js project using Bun:

```bash
bun create next-app@latest my-app   --typescript   --tailwind   --biome   --app   --src-dir   --import-alias "@/*"   --use-bun   --empty

cd my-app
bun install
bun run dev
```

---

## 5) Apply this blueprint overlay

Copy/merge the blueprint files/folders into your new repo root.

Avoid blindly overwriting existing files; prefer selective merges and review diffs.

- `AGENTS.md`
- `ARCHITECTURE.md`
- `.codex/`
- `docs/`
- `reports/`
- `.github/`

Then create the **canonical project docs**:

1) Product specs (what + acceptance criteria)
   - Start with: `docs/product-specs/index.md`
   - Create at least one feature spec from: `docs/product-specs/_TEMPLATE.md`

2) Design System (tokens + primitives)
   - Create: `docs/DESIGN_SYSTEM.md` from `docs/templates/DESIGN_SYSTEM_TEMPLATE.md`

3) Technical Spec (pinned decisions)
   - Create: `docs/TECH_SPEC.md` from `docs/templates/TECH_SPEC_TEMPLATE.md`

Optional:

- Create a design decision record in `docs/design-docs/` for high-impact decisions.
- Keep `ARCHITECTURE.md` as a short map with links to these docs.

Finally:

1) Set `docs/exec-plans/active/NOW.md` to exactly **one** next step.
2) Keep longer lists in your issue tracker (or use `NOW.md → Parking lot`).
3) Run the first checkpoint in a fresh Codex thread.

---

## 6) Optional: Context7 MCP (latest package docs)

If you want the agent to reliably follow the **latest library documentation**, enable a single MCP server (Context7 is a good default).

Rules:

- Treat MCP as **on-demand**: use it when changing dependencies or using a library in a non-trivial way.
- Still prefer **official docs** as the source of truth.
- Record “used Context7” in the checkpoint report when it materially influenced an implementation.
