# 🦞 OpenClaw Starter

A practical guide to building your first personal AI agent — or adding a new one to an existing multi-agent setup.

OpenClaw is a lightweight framework for running AI agents that manage real life: home operations, career planning, health, finances, communications. No app required. No platform lock-in. Just files, a language model, and a clear system for keeping agents focused, safe, and useful over time.

This repo gives you the templates, the architecture, and the step-by-step guides to build your own.

---

## What is OpenClaw?

OpenClaw is a personal AI operating system built on a simple idea: **your agents should be as well-defined as your best employees.**

Every agent in an OpenClaw setup has:
- A clear identity and role (`SOUL.md`)
- A defined set of workflows (`SYSTEMS.md`)
- A trigger and scheduling system (`HEARTBEAT.md`)
- A technical reference (`TOOLS.md`)
- A workspace hierarchy that resolves conflicts (`AGENTS.md`)
- Hard security rules that cannot be overridden by conversation

Agents share state through files and Google Docs — not session history. This means they survive session resets, stay cheap to run, and can hand off context to each other cleanly.

---

## Who this is for

**Path A — Starting from zero:**
You want a personal AI agent that handles daily operations — morning briefings, email triage, calendar, meal planning, reminders. You have a Claude account and about 30 minutes. Start with [QUICKSTART.md](./QUICKSTART.md).

**Path B — Adding to an existing setup:**
You already have agents running and want to add a new one, or wire up a multi-agent system with a shared gateway. Start with [ARCHITECTURE.md](./ARCHITECTURE.md).

---

## The OpenClaw Agent Roster (example)

This is what a full personal OpenClaw setup can look like. You don't need all of these — start with one.

| Agent | Role | Trigger |
|-------|------|---------|
| 🌻 Heidi | Home chief of staff | Daily, on "good morning" |
| 🌿 Sage | Health & nutrition | Weekly, Saturday EOD |
| 💰 Finn | Financial ops | Daily, proactive |
| 🧭 Norah | Career planning | Weekly, on demand |
| ⚙️ Frank | Session ops | Nightly, 3 AM reset |

Each agent is a separate Claude session with its own workspace files. Frank is the ops agent — he resets Heidi's session nightly and re-injects only the context she needs to resume, keeping costs predictable.

---

## Core Concepts

**Files are memory, not session history.**
Claude wakes up fresh every session. Your agent's continuity comes from well-maintained files — not conversation history. If something matters, write it down. Session history is dead weight.

**Security rules don't bend.**
Every OpenClaw agent ships with anti-social-engineering rules baked in. No passphrase, no send. Urgency never lowers the bar — it raises it. These rules cannot be overridden by conversation.

**Shared state, not shared sessions.**
Multi-agent coordination happens through shared Google Docs and workspace files. Agents don't share sessions — they share truth through files.

**One file hierarchy, no conflicts.**
Every workspace has a clear authority order. When rules conflict, the hierarchy resolves it. Child safety beats everything. Identity beats mechanics. Mechanics beat procedures.

---

## Repo Structure

```
openclaw-starter/
├── README.md              # You are here
├── QUICKSTART.md          # Zero to first agent in 30 minutes
├── ARCHITECTURE.md        # Multi-agent design and gateway patterns
├── templates/             # Blank agent workspace templates
│   ├── AGENTS.md
│   ├── SOUL.md
│   ├── HEARTBEAT.md
│   ├── SYSTEMS.md
│   ├── TOOLS.md
│   └── USER.md
├── examples/
│   ├── home-agent/        # Heidi-style personal chief of staff
│   ├── work-agent/        # Professional operations agent
│   └── multi-agent/       # Frank + Heidi nightly reset pattern
├── scripts/
│   ├── google_auth.py     # Google Workspace OAuth setup
│   └── test_google.py     # Verify Google API connectivity
└── docs/
    ├── adding-google.md   # Google Workspace integration
    ├── telegram-setup.md  # Telegram as your primary channel
    ├── session-costs.md   # Managing costs with nightly resets
    └── multi-agent.md     # Adding agents to a single gateway
```

---

## Quick Cost Reference

Running agents on Claude is affordable if you manage session length. Here's what to expect:

| Setup | Est. cost/month |
|-------|----------------|
| Single agent, well-managed sessions | $15–30 |
| Single agent, unmanaged (no resets) | $100–200+ |
| Multi-agent with Frank-style resets | $30–60 |

The Frank pattern (nightly session reset + context re-injection) is the single biggest cost optimization. A session running for 6+ days can hit $150 in a week. The same workload with daily resets costs $5–15/session.

See [session-costs.md](./docs/session-costs.md) for the full breakdown.

---

## Getting Started

→ [QUICKSTART.md](./QUICKSTART.md) — build your first agent in 30 minutes
→ [ARCHITECTURE.md](./ARCHITECTURE.md) — understand the multi-agent model
→ [examples/home-agent/](./examples/home-agent/) — see a full Heidi-style setup

---

## Based On

This framework was built and battle-tested running a personal household agent system since early 2026. The patterns here aren't theoretical — they come from operating real agents with real costs, real security considerations, and real failure modes.

The original Heidi workspace is at [github.com/kaitwaite/heidi](https://github.com/kaitwaite/heidi).

---

*Built by Kate Haan · [katehaan.dev](https://katehaan.dev) · [LinkedIn](https://www.linkedin.com/in/katehaan/)*
