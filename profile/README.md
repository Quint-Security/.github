# Quint

**Control what AI agents can do. Prove what they did.**

AI agents call tools with no permissions, no audit trail, and no accountability. Quint fixes that — one config line, zero agent changes.

```
AI Agent  →  Quint  →  MCP Server
               ↑
         enforce policy
         sign every action
         log to tamper-evident chain
```

## Install

```bash
npm install -g @quint-security/cli
quint keys generate && quint policy init
```

Then wrap any MCP server:

```json
{ "command": "quint", "args": ["proxy", "--name", "my-server", "--", "my-mcp-server"] }
```

The agent doesn't know Quint exists. Every tool call is now policy-checked, signed, and logged.

## What you get

- **Allow/deny policy** per server, per tool, with glob patterns (`write_*`, `Mechanic*`)
- **Cryptographic audit trail** — every action signed with Ed25519, hash-chained in SQLite
- **Independent verification** — export the log, hand it to anyone, they can verify what happened
- **Fail-closed** — no policy match means deny

## Repos

- **[cli](https://github.com/Quint-Security/cli)** — proxy, audit log viewer, key management, policy engine (TypeScript)
- **[proto](https://github.com/Quint-Security/proto)** — protobuf schema definitions shared across components

## Architecture

Two runtime dependencies: `better-sqlite3` + `commander`. Crypto is `node:crypto` built-in (Ed25519 + SHA-256). Works with any MCP-compatible agent — Claude Code, Cursor, Cline, Codex.

## Links

- [Documentation](https://github.com/Quint-Security/cli#readme)
