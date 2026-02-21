# Quint Security

Local security proxy for AI agent tool calls — control what agents can do, prove what they did.

## The Problem

AI agents (Claude Code, Cursor, Codex) call tools with no granular permissions, no audit trail, and no way to prove a human authorized a specific action. As agents go autonomous, this is a real security gap.

## What Quint Does

Quint sits between AI agents and their MCP tool servers, intercepting every JSON-RPC message in the pipe:

```
AI Agent  →  Quint Proxy  →  Real MCP Server
                ↑
          Parse every message
          Check policy (allow/deny)
          Sign with Ed25519
          Log to SQLite
```

- **One config line change** to enable — agents don't know Quint exists
- **Allow/deny policy** per server, per tool, with glob patterns (`Mechanic*`, `write_*`)
- **Cryptographic audit trail** — every action signed with Ed25519, hash-chained, tamper-evident
- **Independently verifiable** — hand someone the log and they can prove what happened

## Repos

| Repo | What | Language |
|------|------|----------|
| [quint-cli](https://github.com/Quint-Security/quint-cli) | CLI tools — proxy, audit log viewer, signature verification, policy management | TypeScript |
| [quint-proto](https://github.com/Quint-Security/quint-proto) | Protobuf schema definitions — shared contract between all components | Protobuf |
| [quint-proxy](https://github.com/Quint-Security/quint-proxy) | Core proxy daemon (WIP) | Go |

## Quick Start

```bash
git clone https://github.com/Quint-Security/quint-cli.git
cd quint-cli
npm install && npm run build && npm link

quint keys generate
quint policy init
quint status
```

Then proxy an MCP server through Quint:

```json
{ "command": "quint", "args": ["proxy", "--name", "my-server", "--", "my-mcp-server"] }
```

## Architecture

- **2 runtime dependencies** — `better-sqlite3` + `commander`
- **Zero external crypto** — Ed25519 and SHA-256 via Node.js built-in `node:crypto`
- **Fail-closed** — no policy match = deny
- **Provider-neutral** — works with any MCP-compatible agent

## Setup

### 1. Git Clone Shortcut

Add the Quint URL alias so you can clone any org repo with `git clone @quint/<repo>`:

```bash
git config --global url."git@github.com:Quint-Security/".insteadOf "@quint/"
```

Then clone this repo:

```bash
git clone @quint/skills
```

### 2. Install Skills Locally

Symlink all skills into Claude Code so they're available as slash commands (e.g. `/golang-expert`):

```bash
make skills.inject
```

Symlinks stay in sync with the repo — `git pull` automatically updates your local commands. You only need to re-run this after new skills are added.

