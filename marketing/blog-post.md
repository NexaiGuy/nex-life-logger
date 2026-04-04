---
title: I Built an AI Agent Skill That Remembers Everything You Do on Your Computer
published: true
description: Privacy-first local activity tracking with AI-powered summaries. 67K+ activities tracked, zero data sent to the cloud.
tags: ai, productivity, opensource, privacy
cover_image: https://raw.githubusercontent.com/NexaiGuy/nex-life-logger/main/screenshots/ai-search.png
---

# I Built an AI Agent Skill That Remembers Everything You Do on Your Computer

AI agents are powerful. But they have a blind spot: they start every conversation from zero. They don't know what you were researching yesterday, which YouTube tutorial explained that technique you need, or how you solved a similar problem last month.

I wanted to fix that. So I built **Nex Life Logger**, a background activity tracker that gives your AI agent persistent memory of what you actually do on your computer. It tracks your browsing history, active windows, and YouTube videos, stores everything locally, and lets you query it all through natural language.

67,000+ activities tracked so far. Zero data sent to the cloud.

## The Problem

I run a digital transformation agency in Belgium (Nex AI) and spend my days jumping between code editors, documentation, design tools, YouTube tutorials, and dozens of browser tabs. By Friday, I've forgotten half of what I researched on Monday. I needed a way to ask "What was I working on when I was debugging that Docker issue?" and get an actual answer.

Existing tools like Rewind and Windows Recall either send your data to the cloud or lock you into one platform. For someone who cares about where their data goes, that was a dealbreaker.

## How It Works

Nex Life Logger has a simple architecture. A background collector runs every 30 seconds and captures three things:

**Browser history** from Chrome, Edge, Brave, and Firefox. It copies the locked SQLite history files to temp, reads them, then securely deletes the copies (overwritten with random bytes before unlinking). No browser extension needed.

**Active window focus.** It checks which application and window title are in the foreground. This gives context about what tool you were using, not just what you were browsing.

**YouTube transcripts.** When you watch a productive video, it automatically fetches the full transcript and stores it. This is where the real value is. When the AI generates summaries, it can tell you exactly what was discussed in each video, including the key concepts, tools, and techniques mentioned.

Everything lands in a local SQLite database at `~/.life-logger/`. WAL mode for crash safety, owner-only file permissions, no external connections.

## The Filtering Layer

Tracking everything would be a privacy nightmare. So there are multiple filtering layers:

Chat and messaging apps are excluded automatically. WhatsApp, Discord, Slack, Telegram, Signal, Teams, and anything with `/messages`, `/chat`, or `/dm` in the URL. Sensitive windows too: password managers, banking apps.

There's also a productivity filter. The system only tracks content related to AI, programming, design, building, and learning. Politics, news, entertainment, sports, and celebrity gossip are automatically filtered out. You can configure all of this through 12 customizable filter categories.

## AI-Powered Summaries

Raw activity data is useful but noisy. The real power comes from hierarchical AI summaries.

Every night at 11 PM, the system generates a daily summary from that day's raw activities and transcripts. On Sundays, it generates a weekly summary from the daily ones. On the 1st of each month, a monthly summary from the weeklies. On January 1st, a yearly summary from the monthlies.

Each level builds on the one below it, creating a compressed but rich record of everything you've done. After a few weeks, you have a layered memory system that an AI can search through instantly.

The summarization works with any OpenAI-compatible API. I'm running it with Alibaba's Qwen (free tier), but you can use OpenAI, Groq, Ollama for fully local, or any compatible endpoint.

## Querying Your History

There are two ways to query your data.

**The desktop app** has a built-in AI Search tab. Type a question like "What was I researching about Docker last week?" and it searches across activities, summaries, keywords, and transcripts, then generates an answer with specific dates, links, and context.

**The OpenClaw/ClawHub skill** lets you query through any connected agent, whether that's Telegram, Discord, or WhatsApp. I published the skill to ClawHub (the OpenClaw skill registry) so anyone running OpenClaw can install it with one command:

```bash
npx clawhub install nex-life-logger
```

Then you message your agent naturally. "What was I working on yesterday?" and it calls the CLI, searches your local database, and answers in the conversation.

## The CLI

The ClawHub skill includes a full CLI for querying your data directly:

```bash
nex-life-logger search "docker containers"
nex-life-logger summary daily
nex-life-logger activities --last 2h --kind youtube
nex-life-logger keywords --category tool --top 15
nex-life-logger stats
```

There are commands for searching, browsing activities, viewing summaries, extracting keywords, managing the background collector, configuring AI providers, and exporting your data in JSON, CSV, or HTML.

## What I Learned Building It

**SQLite is perfect for this use case.** Fast writes, zero configuration, single file backups. With WAL mode, the collector and the viewer can read and write simultaneously without conflicts.

**Content filtering is harder than expected.** The productivity filter went through multiple iterations. Pure keyword matching catches obvious cases but misses nuance. I added an optional AI-based classifier for ambiguous content, but kept it off by default to avoid unnecessary API costs.

**YouTube transcripts are gold.** The daily summaries became 10x more useful once they included what was discussed in videos. Instead of "watched 3 YouTube videos about Docker," you get "watched a tutorial on multi-stage Docker builds covering layer caching, build arguments, and image optimization for production."

**Privacy-first isn't just a feature, it's a design constraint.** Every decision was filtered through "does this keep data local?" No cloud sync, no telemetry, no analytics. The API key is stored in Windows Credential Manager, not a config file. Browser history files are securely deleted after reading. It adds complexity, but it's the right tradeoff.

## What's Next

The current version tracks browsers and windows. I'm considering adding:

- **Clipboard history** (what you copy and paste throughout the day)
- **Terminal commands** (your shell history with context)
- **File system changes** (what files you created, modified, deleted)
- **Calendar integration** (correlate activities with meetings)

Each one adds another dimension to the agent's memory of your workday.

## Try It

**Desktop app (Windows, macOS, Linux):**
[GitHub: NexaiGuy/nex-life-logger](https://github.com/NexaiGuy/nex-life-logger)

**OpenClaw/ClawHub skill (one-command install):**
```bash
npx clawhub install nex-life-logger
```
[ClawHub: nex-life-logger](https://clawhub.ai/nexaiguy/nex-life-logger)

Built by [Nex AI](https://nex-ai.be), a digital transformation agency in Belgium. If you work with AI agents and want this kind of integration for your business, that's what we do.

What data sources would you want your agent to remember? I'd love to hear what would be most useful.
