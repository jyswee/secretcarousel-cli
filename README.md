# secretcarousel

The agent-first secret vault. Store, rotate, and share secrets from any coding agent.

## Install

```bash
npm install -g secretcarousel
```

Or run directly:

```bash
npx secretcarousel signup my-project --local
```

## Quick Start

```bash
# Self-provision a tenant (key saved to .sc/config.json)
sc signup my-project --local

# Store a secret (AES-256-GCM encrypted at rest)
sc secret "DB_URL" "postgres://user:pass@host/db" -t database-credentials

# Retrieve (decrypted on demand)
sc secret show sec-abc123

# List all secrets
sc secrets

# Export as .env
sc env pull --env production > .env

# Rotate immediately
sc rotate sec-abc123

# Share with another agent (time-limited link)
sc share sec-abc123 --hours 1 --views 1
```

## Commands

**Getting Started**
| Command | Description |
|---------|-------------|
| `signup <tenant> [--local]` | Self-provision a tenant |
| `login --key KEY [--local]` | Store API key |
| `logout [--local]` | Clear config |
| `me` | Show tenant info + plan + usage |
| `config` | Show active config source |
| `status` | Project overview |

**Secrets**
| Command | Description |
|---------|-------------|
| `secret "NAME" "VALUE" [-t TYPE]` | Create a secret |
| `secret show <ID>` | Get decrypted value |
| `secret update <ID> --value NEW` | Update (new version) |
| `secret delete <ID>` | Delete |
| `secrets [--type X] [--env X]` | List all |

**Operations**
| Command | Description |
|---------|-------------|
| `rotate <ID>` | Rotate now |
| `rotate set <ID> --schedule "30d"` | Set rotation policy |
| `share <ID> [--hours 1] [--views 1]` | Create share link |
| `shares` | List active shares |
| `claim "VALUE" --to T --contract C` | Create claim token |
| `claim redeem <TOKEN>` | Claim a token |
| `claims` | List claim tokens |

**Environment**
| Command | Description |
|---------|-------------|
| `env pull [--env production]` | Export as .env |
| `env promote --from X --to Y` | Promote secrets |

**Compliance**
| Command | Description |
|---------|-------------|
| `audit [--action X] [--limit N]` | Query audit trail |
| `audit export [--format csv]` | Export audit log |
| `backup [--name X]` | Create encrypted backup |
| `backups` | List backups |

## Configuration

Config priority (first match wins):

1. `--key` flag (inline)
2. `SC_API_KEY` environment variable
3. `.sc/config.json` (local project)
4. `~/.secretcarousel/config.json` (global)

```bash
# Environment variable (recommended for CI/agents)
export SC_API_KEY=sc_free_my_project_a1b2c3...

# Or store permanently
sc login --key sc_free_my_project_a1b2c3...

# Per-project config (auto-loaded, add .sc/ to .gitignore)
sc login --key sc_free_... --local
```

## Output

Human-readable output by default. Add `--json` for structured JSON:

```bash
sc secrets --json    # JSON array
sc me --json         # JSON object
```

## Features

- AES-256-GCM encrypted storage with unique keys per secret
- Automatic version history on every update
- Cron-based or on-demand secret rotation
- Time-limited, view-limited share links with passphrase protection
- Cross-agent secret exchange via Buggazi claim tokens
- Immutable audit trail with CSV/JSON export
- Encrypted backups with per-backup keys
- Zero dependencies (Node.js 18+ built-in fetch)

## Links

- Quickstart: https://secretcarousel.com/docs/quickstart.html
- API Reference: https://secretcarousel.com/api
- Pricing: https://secretcarousel.com/#pricing

## License

Proprietary. Copyright (c) 2026 Tyga.Cloud Ltd (Company No. 14643275).
See LICENSE file for full terms including indemnification and liability provisions.
