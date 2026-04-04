# Social Media Launch Drafts

## Reddit Posts

### r/OpenClaw (Post first, morning)

**Title:** I built a skill that gives your agent memory of everything you do on your computer

**Body:**

Been building this for a few weeks and just published it to ClawHub: **nex-life-logger**

It's a background activity tracker that runs on your machine and gives your OpenClaw agent the ability to answer questions about what you've been doing. Browser history, active windows, YouTube videos with full transcript capture. Everything stays local in a SQLite database.

Install: `npx clawhub install nex-life-logger`

Then you can ask your agent things like:
- "What was I working on yesterday afternoon?"
- "Search my history for Docker"
- "What YouTube videos did I watch about machine learning?"
- "Show me my productivity summary for last week"

The agent calls the CLI under the hood, searches your local database, and answers naturally.

**How it works:**

A background collector polls every 30 seconds. Reads browser history from Chrome/Edge/Brave/Firefox, tracks active window focus, and fetches YouTube transcripts automatically. Content goes through a productivity filter (only tracks AI, programming, design, learning content, skips politics/news/entertainment). Chat apps and sensitive windows (password managers, banking) are excluded automatically.

AI summaries are generated on a schedule: daily at 11 PM, weekly on Sunday, monthly on the 1st, yearly on Jan 1. Each level summarizes the one below it. You can also generate them on demand.

Works with any OpenAI-compatible API for the AI features (Qwen, OpenAI, Groq, Ollama, etc.). The tracking, search, stats, and keyword commands work without any API key.

**Privacy angle:** No cloud. No account. No telemetry. Your data lives in `~/.life-logger/` and nowhere else. I built this because every similar tool (Rewind, Recall) sends data somewhere or locks you into a platform.

ClawHub: https://clawhub.ai/nexaiguy/nex-life-logger
GitHub: https://github.com/NexaiGuy/nex-life-logger

Would love feedback. What other data sources would be useful to track?

---

### r/selfhosted (Post second, afternoon)

**Title:** Self-hosted activity tracker that runs as an AI agent skill. All data stays on your machine.

**Body:**

Built a local activity tracker called Nex Life Logger. It captures browser history, active windows, and YouTube transcripts, stores everything in SQLite, and generates AI-powered summaries. No cloud, no account, no subscription.

Designed it for my own use first, then packaged it as an OpenClaw/ClawHub skill so my Telegram AI agent can query it. I ask "What was I working on yesterday?" and the agent searches my local database and answers.

**What it tracks:**
- Browser history (Chrome, Edge, Brave, Firefox)
- Active window focus (every 30 seconds)
- YouTube transcripts (automatic for productive videos)
- Search queries

**What it filters out:**
- All chat/messaging (WhatsApp, Discord, Slack, Telegram, Signal, Teams)
- Sensitive windows (password managers, banking)
- Non-productive content (politics, news, entertainment)

**Self-hosted details:**
- SQLite database in `~/.life-logger/`
- systemd user service on Linux
- LaunchAgent on macOS
- No external dependencies beyond Python 3.11+
- Works with local LLMs via Ollama (no API key needed for that)
- All data stays on your machine

Runs on my Raspberry Pi as part of my OpenClaw setup, collecting data and serving queries through Telegram.

GitHub: https://github.com/NexaiGuy/nex-life-logger
ClawHub: https://clawhub.ai/nexaiguy/nex-life-logger

---

### r/ClaudeAI (Day 2)

**Title:** Built a ClawHub skill that tracks your activity and lets you query it with AI (v1.1.0, now with FTS5 search)

**Body:**

Just pushed v1.1.0 of nex-life-logger, a ClawHub skill that gives your AI agent persistent memory of what you do on your computer.

It runs a background collector that tracks browser history, active windows, and YouTube videos (with full transcripts). Then your agent can query all of it through natural language. Ask "What was I researching last week?" and it searches your local SQLite database and answers.

v1.1.0 just added FTS5 full-text search with Porter stemming, so searching "containers" now matches "container", "containerized", etc. You can also filter by source (`--source chrome`), activity type (`--kind youtube`), and get JSON output for programmatic use (`--output json`). Results are ranked by relevance (text match quality + recency).

The AI features work with any OpenAI-compatible API. I'm running it with Qwen (free tier) on my Raspberry Pi setup, but you can use OpenAI, Groq, Ollama, or anything compatible.

Install: `npx clawhub install nex-life-logger`

Privacy-first: everything stays local. No cloud, no account, no data leaving your machine. 67K+ activities tracked so far.

GitHub: https://github.com/NexaiGuy/nex-life-logger
ClawHub: https://clawhub.ai/nexaiguy/nex-life-logger

---

### r/SideProject (Day 2-3)

**Title:** Side project: an AI agent skill that gives your computer a memory (v1.1.0 with FTS5 search)

**Body:**

I run a digital transformation agency in Belgium (Nex AI) and built this as a tool I wanted for myself: a background activity tracker that lets my AI agent answer questions about my work history.

**The problem:** I kept forgetting what I was researching earlier in the week, which YouTube tutorial covered a specific technique, or how I solved something last month. My AI agent was helpful but had no context about what I actually do day to day.

**The solution:** Nex Life Logger runs silently, collects browser history and active window data, fetches YouTube transcripts, and generates daily/weekly/monthly summaries using AI. Now I can ask my Telegram bot "What was I working on yesterday?" and get an actual answer.

Just shipped v1.1.0 with FTS5 full-text search. Searches are way faster now, support Porter stemming (so "deploying" matches "deployment"), and results are ranked by relevance + recency. Also added filters so I can drill down: `search "react" --kind url --source chrome --output json`.

Published it to ClawHub (the OpenClaw skill registry) and also put it on GitHub. Got 67K+ activities tracked so far.

What I learned building it:
- SQLite is perfect for this. Fast, zero config, single file backup. FTS5 extension is a game changer for search quality.
- Content filtering is harder than expected. The productivity filter took multiple iterations
- YouTube transcripts are gold. The AI summaries are 10x more useful when they include what was discussed in videos
- Privacy-first isn't just a feature, it's a requirement. Nobody wants their browsing history in the cloud

GitHub: https://github.com/NexaiGuy/nex-life-logger
ClawHub: https://clawhub.ai/nexaiguy/nex-life-logger

---

## Hacker News

**Title:** Show HN: Nex Life Logger, local activity tracker with AI agent integration

**Link:** https://github.com/NexaiGuy/nex-life-logger

**First comment (post immediately):**

Hey HN. I built Nex Life Logger because I wanted my AI agent to have context about what I actually do on my computer.

It's a background activity tracker that captures browser history (Chrome/Edge/Brave/Firefox), active window focus, and YouTube video transcripts. Everything goes into a local SQLite database. No cloud, no account, no telemetry.

On top of the raw data, it generates hierarchical AI summaries: daily at 11 PM, weekly on Sunday, monthly on the 1st, yearly on Jan 1. Each level summarizes the one below it. Works with any OpenAI-compatible API (OpenAI, Qwen, Groq, Ollama for fully local).

The AI search lets you query your entire history in natural language. Ask "What was I researching about Docker last week?" and it searches activities, summaries, keywords, and transcripts, then generates an answer.

I also packaged it as a ClawHub skill for OpenClaw, so it integrates with Telegram/Discord/WhatsApp agents. One-command install: `npx clawhub install nex-life-logger`.

Privacy decisions: all chat/messaging apps are excluded automatically (WhatsApp, Discord, Slack, etc.). Sensitive windows (password managers, banking) are never logged. There's a productivity filter that only tracks AI, programming, design, and learning content, though you can configure what passes through.

Technical stack: Python 3.11, SQLite (WAL mode), pystray + Pillow for the tray icon, pywebview for the desktop viewer, youtube-transcript-api for transcripts, openai SDK for LLM calls.

What other data sources would people want tracked? I'm considering clipboard history, terminal commands, and file system changes for v2.

---

## X (Twitter) Thread

**Tweet 1 (hook):**
I just published an OpenClaw skill that gives your AI agent memory of everything you do on your computer.

Local-only. No cloud. Privacy-first. One command to install.

clawhub.ai/nexaiguy/nex-life-logger

**Tweet 2 (demo):**
Here's what it looks like:

I ask my Telegram agent "What was I working on yesterday?"

It searches my local activity database, finds browser history + active windows + YouTube transcripts, and answers naturally.

[Attach screen recording / screenshot of Telegram conversation]

**Tweet 3 (technical):**
Under the hood:

A background collector reads browser history (Chrome, Edge, Brave, Firefox) and tracks active windows every 30 seconds.

Everything goes into a local SQLite database.

AI generates daily/weekly/monthly summaries. Each level builds on the one below it.

**Tweet 4 (privacy):**
Unlike Rewind or Windows Recall, nothing leaves your machine.

No account. No subscription. No cloud storage.

Your data stays in ~/.life-logger/ and nowhere else.

Chat apps, password managers, and banking windows are automatically excluded.

**Tweet 5 (install):**
Install it:
npx clawhub install nex-life-logger

Or check it out on GitHub:
github.com/NexaiGuy/nex-life-logger

Works with any OpenAI-compatible API. Or use Ollama for fully local AI.

**Tweet 6 (builder):**
Built this at Nex AI, my digital transformation agency in Belgium.

This is the kind of AI integration I build for clients. If you're an SME looking to actually use AI (not just talk about it), check out nex-ai.be

**Tweet 7 (engagement):**
What other data would you want your agent to remember?

Thinking about adding:
- Clipboard history
- Terminal commands
- File system changes
- Calendar events
- Email metadata

What would be most useful?

#OpenClaw #AIAgents #LocalFirst #PrivacyFirst #BuildInPublic

---

## LinkedIn

I just published something that changes how I work with AI agents.

AI agents are powerful. But they have a blind spot: they don't know what you actually do on your computer. Every conversation starts from zero.

I built Nex Life Logger to fix that. It silently tracks your browser history, active windows, and YouTube videos. Stores everything locally in a SQLite database. Generates AI-powered summaries daily, weekly, monthly.

Now when I message my AI agent on Telegram and ask "What was I working on yesterday?" it searches my activity database and gives me a real answer. With context about which tools I used, what I researched, and what was discussed in the videos I watched.

Privacy was non-negotiable. All data stays on my machine. No cloud sync, no account, no telemetry. Chat apps and sensitive windows are automatically excluded.

Published it as an open-source skill on ClawHub (the OpenClaw skill registry) and on GitHub. Already tracking 67,000+ activities.

This is the kind of AI integration I build daily at Nex AI for Belgian SMEs. Not theoretical AI, but tools that actually make you more productive.

Try it: clawhub.ai/nexaiguy/nex-life-logger
Code: github.com/NexaiGuy/nex-life-logger

#AI #Productivity #OpenSource #AIAgents #DigitalTransformation #LocalFirst #PrivacyFirst #BuildInPublic

---

## Dev.to / Medium Article

**Title:** I Built an AI Agent Skill That Remembers Everything You Do on Your Computer

**Subtitle:** Privacy-first local activity tracking with AI-powered summaries. 67K+ activities tracked, zero data sent to the cloud.

[Full 1000-1500 word article to be written separately based on the structure in the marketing strategy doc]

---

## awesome-openclaw-skills PR

**Category:** Productivity

**Entry:**
```markdown
- [nex-life-logger](https://clawhub.ai/nexaiguy/nex-life-logger) - AI-powered local activity tracker. Tracks browser history, active windows, and YouTube videos. Query your history through your agent. Privacy-first, all data stays local. ([GitHub](https://github.com/NexaiGuy/nex-life-logger))
```
