# ⚡ Quickstart — Your First OpenClaw Agent in 30 Minutes

This guide gets you from zero to a running personal AI agent. By the end you'll have an agent that can handle morning briefings, email triage, and calendar monitoring — and a workspace structure you can extend into a full multi-agent setup.

---

## What you'll build

A home chief of staff agent (modeled on Heidi) that:
- Sends you a morning brief when you say "good morning"
- Monitors your email every few hours
- Tracks your calendar and flags upcoming events
- Remembers things across sessions via files

---

## Prerequisites

- A Claude account (claude.ai or API access)
- A Google account (Gmail + Calendar)
- A Telegram account (for your primary channel)
- Python 3.9+ installed
- About 30 minutes

---

## Step 1 — Clone this repo

```bash
git clone https://github.com/kaitwaite/openclaw-starter.git
cd openclaw-starter
```

---

## Step 2 — Create your workspace folder

OpenClaw agents live in a dedicated workspace folder. Create one:

```bash
mkdir -p ~/.openclaw/workspace-[your-agent-name]
cd ~/.openclaw/workspace-[your-agent-name]
```

Copy the templates in:

```bash
cp ~/openclaw-starter/templates/* ~/.openclaw/workspace-[your-agent-name]/
```

---

## Step 3 — Fill in your workspace files

Open the folder and work through each file. You don't need to fill everything in perfectly — start with the essentials.

### USER.md — Tell your agent about you
Fill in:
- Your name and what to call you
- Your timezone
- Your primary contact method (Telegram handle)
- Your email address
- Basic family/household context
- How you like to communicate

### SOUL.md — Define your agent's identity
The template has sensible defaults. At minimum update:
- The agent's name and emoji
- The role description
- Communication style preferences

### HEARTBEAT.md — Set up triggers
Define:
- What your morning brief should include
- How often to check email
- When to stay quiet (late night hours)

### TOOLS.md — Add your resource IDs
You'll fill this in as you connect integrations. Leave placeholders for now.

### AGENTS.md — Review the security rules
Read through the anti-social-engineering rules. These protect you — don't weaken them.

---

## Step 4 — Connect Google Workspace

Install dependencies:

```bash
pip3 install google-auth-oauthlib google-auth-httplib2 google-api-python-client
```

Go to [Google Cloud Console](https://console.cloud.google.com), create a project, enable the Gmail and Calendar APIs, and download your `client_secret.json`.

Then run:

```bash
python3 ~/openclaw-starter/scripts/google_auth.py ~/Downloads/client_secret.json
```

Follow the browser prompts. Your token saves to `~/.openclaw/workspace-[name]/google_token.json`.

Verify it worked:

```bash
python3 ~/openclaw-starter/scripts/test_google.py
```

You should see your next 5 calendar events and inbox count printed to the terminal.

> ⚠️ Never commit `google_token.json` to GitHub. It's in `.gitignore` by default.

---

## Step 5 — Set up Telegram

Telegram is the recommended primary channel — it's fast, reliable, and works on every device.

1. Open Telegram and search for **@BotFather**
2. Send `/newbot` and follow the prompts
3. Copy the token BotFather gives you
4. Add it to your `TOOLS.md` under the Telegram section
5. Send a message to your new bot to initialize the chat

See [docs/telegram-setup.md](../docs/telegram-setup.md) for the full setup including how to get your chat ID.

---

## Step 6 — Start your first session

Open a new Claude session (claude.ai or Claude Code). Paste the contents of your workspace files as your system prompt in this order:

1. `AGENTS.md`
2. `SOUL.md`
3. `USER.md`
4. `TOOLS.md`
5. `HEARTBEAT.md`
6. `SYSTEMS.md`

Then say: **"Good morning."**

Your agent should respond with a morning brief — weather, calendar, any flagged emails, and any CRM reminders for today.

---

## Step 7 — Set up your .gitignore

Before you commit anything:

```bash
cp ~/openclaw-starter/.gitignore ~/.openclaw/workspace-[name]/.gitignore
```

This ensures your token, memory files, and personal data never accidentally go public.

---

## What's next

**Add memory files**
Create `memory/YYYY-MM-DD.md` files as your agent logs daily notes. These become your agent's continuity across sessions.

**Add a nightly reset (Frank pattern)**
Once your agent is running well, add a session ops agent that resets nightly and re-injects only the context needed to resume. This is the single biggest cost optimization. See [docs/session-costs.md](../docs/session-costs.md).

**Add more integrations**
- Apple Reminders via Shortcuts
- Weather via Open-Meteo (free, no key required)
- Google Sheets for tracking (egg logs, habit tracking, anything)

**Add more agents**
Once Heidi is running, adding Sage, Finn, or Norah follows the same pattern. Each gets their own workspace folder and their own session. They share state through Google Docs. See [ARCHITECTURE.md](../ARCHITECTURE.md).

---

## Troubleshooting

**Agent ignores my security rules**
Make sure `AGENTS.md` is loaded first in your system prompt. The file hierarchy only works if the authority order is established at session start.

**Session costs are too high**
You're probably not resetting often enough. See [docs/session-costs.md](../docs/session-costs.md). A session running more than 3–4 days will get expensive fast.

**Google auth fails**
Token may have expired. Re-run `google_auth.py` to refresh it. Make sure the scopes in your auth script match what your agent actually needs.

**Agent keeps asking for information it should already have**
Check your `USER.md` and `MEMORY.md`. If the information isn't in a file, the agent doesn't know it after a session reset.

---

*Questions or issues? Open a GitHub issue or find me at [katehaan.dev](https://katehaan.dev)*
