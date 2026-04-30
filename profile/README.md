# Quint

**Behavioral security for AI agents.**

One install. Every agent. Every action. Zero code changes.

---

## The gap

In July 2025, Replit's AI agent deleted a production database during a code freeze, then fabricated 4,000 fake users to cover its tracks. The proxy logs said it was editing files. The kernel knew it had run `DROP TABLE`.

That gap — between what an agent claims and what the OS actually sees — is where every AI agent breach lives. Existing tools stop at the API gateway. We don't.

## The idea

A single action is never the signal. The sequence is.

"Read config" is fine. "Read config → open network socket → touch `~/.ssh`" is a breach in progress. Quint scores the whole story, not each call in isolation.

## What Quint does

- **OS-level interception** across macOS and Linux — every filesystem, process, and network call
- **Behavioral baselines** per agent, per user, per fleet — deviation is the signal
- **Real-time risk scoring** in under 10 milliseconds, at the edge
- **Policy enforcement** — block, flag, or allow before the damage lands
- **Tamper-proof audit** — Ed25519-signed, hash-chained records for every tool call
- **Fleet management** — one control plane across every agent in your org

## What Quint catches

- MCP tool poisoning
- In-process subagent spawning — one session silently forking into many
- Proxy/kernel divergence — agent says it called Bedrock, kernel says it read `~/.aws/credentials` first
- Shadow agents running in dev environments IT never approved

## Works with

Claude Code · Cursor · GitHub Copilot · Windsurf · Cline · Aider · Continue · Amazon Q Developer · Gemini CLI — and any agent running on macOS or Linux.

## Compliance

Maps to GDPR, HIPAA, SOC 2, PCI-DSS, EU AI Act, NIST AI RMF, and ISO 42001.

## Privacy

Edge-first by design. Raw agent conversations, tool arguments, and file contents never leave the endpoint. Only structured metadata — action type, risk score, timestamps — reaches the cloud.

## Links

| | |
|---|---|
| Website | [quintai.dev](https://quintai.dev) |
| Blog | [quintai.dev/blog](https://quintai.dev/blog) |
| Platform | [quintai.dev/platform](https://quintai.dev/platform) |
| Security & trust | [quintai.dev/security](https://quintai.dev/security) |
| Book a demo | [quintai.dev/demo](https://quintai.dev/demo) |
| LinkedIn | [linkedin.com/company/quint-security](https://linkedin.com/company/quint-security) |
| X | [@QuintSecurity](https://x.com/QuintSecurity) |
| Contact | hello@quintai.dev |

---

<sub>We audit the agent, not the developer.</sub>
