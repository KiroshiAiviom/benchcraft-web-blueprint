# Context7 MCP (up-to-date docs)

Purpose: reduce API drift by letting Codex consult version-specific documentation and examples.

Context7 complements web search, especially when you need exact signatures or recently changed APIs.

## Configure once, use everywhere

Codex surfaces share MCP configuration (app, IDE extension, CLI). Configure it in whichever surface you prefer.

## Option A — Add via Codex App (recommended)

1) Open Codex app → **Settings** → **MCP**.
2) Add a server named `context7` that runs:

```bash
npx -y @upstash/context7-mcp
```

Commit the resulting `.codex/` config file(s) to share across the project/team.

## Option B — Add via Codex CLI

```bash
codex mcp add context7 -- npx -y @upstash/context7-mcp
```

## Option C — Configure via `.codex/config.toml`

Example:

```toml
[mcp_servers.context7]
command = "npx"
args = ["-y", "@upstash/context7-mcp"]
```

## Usage guidance

- Use Context7 for non-trivial library usage and when implementing against a specific version.
- Prefer it for “what is the correct API shape?” questions over guessing.
