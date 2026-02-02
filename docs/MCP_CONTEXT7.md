# Context7 MCP (up-to-date docs)

Purpose: reduce API drift by letting Codex consult version-specific documentation and examples.

Context7 complements web search, especially when you need exact signatures or recently changed APIs.

## Option A — Add via Codex CLI (recommended)

```bash
codex mcp add context7 -- npx -y @upstash/context7-mcp
```

## Option B — Configure via `.codex/config.toml`

Example:

```toml
[mcp_servers.context7]
command = "npx"
args = ["-y", "@upstash/context7-mcp"]
```

## Usage guidance

- Use Context7 for non-trivial library usage and when implementing against a specific version.
- Prefer it for “what is the correct API shape?” questions over guessing.

