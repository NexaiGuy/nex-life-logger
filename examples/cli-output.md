# Example CLI Output

## Stats

```
$ nex-life-logger stats

Nex Life Logger Statistics
---
Total activities: 67,780
Total summaries: 95
Total keywords: 3,241
Total transcripts: 47
Database size: 82.4 MB

Top sources:
  chrome: 41,203
  window: 18,442
  edge: 5,891
  brave: 2,244

Top types:
  url: 38,127
  app_focus: 18,442
  search: 7,892
  youtube: 3,319
```

## Search

```
$ nex-life-logger search "docker"

Search results for "docker"
---

Activities (23 matches):
- 2026-04-03 14:22 [url] Docker Compose networking guide - docs.docker.com
- 2026-04-03 14:18 [url] docker compose up vs docker-compose up - stackoverflow.com
- 2026-04-03 09:41 [app_focus] VS Code - docker-compose.yml
- 2026-04-02 16:33 [url] Multi-stage Docker builds - docs.docker.com
- 2026-04-02 16:20 [youtube] Docker in 100 Seconds - youtube.com
  ...

Summaries (3 matches):
- 2026-04-03 daily: "...extensive work on Docker Compose configurations, focusing on
  multi-container setups for the SocialHub deployment..."
- 2026-04-02 daily: "...researched Docker multi-stage builds to optimize container
  image sizes for production..."

Transcripts (1 match):
- Docker in 100 Seconds (Fireship): "Docker is a platform for building, running,
  and shipping applications in containers..."
```

## Daily Summary

```
$ nex-life-logger summary daily

Daily Summary - April 3, 2026
---
Today was a productive development day focused on two main areas:

**Infrastructure & DevOps**
Spent the morning configuring Docker Compose for the SocialHub multi-container
deployment. Researched networking between containers, environment variable
injection, and health checks. Referenced the official Docker docs extensively.

**AI Integration**
In the afternoon, shifted to working on the Life Logger ClawHub skill. Spent
time on the CLI tool architecture, testing the search command against the
local database, and writing the SKILL.md documentation for OpenClaw agent
integration.

**YouTube**
Watched 2 technical videos:
- "Docker in 100 Seconds" by Fireship (quick refresher on container concepts)
- "Building AI Agents with Tool Use" (covered function calling patterns)

**Top tools used:** VS Code, Chrome, Docker Desktop, Terminal
**Top topics:** Docker, OpenClaw, ClawHub, Python CLI, AI agents
```

## Keywords

```
$ nex-life-logger keywords --top 10

Top Keywords
---
1. docker (142 mentions) [tool]
2. python (128 mentions) [language]
3. react (97 mentions) [language]
4. openclaw (84 mentions) [tool]
5. firebase (71 mentions) [tool]
6. typescript (63 mentions) [language]
7. ai-agents (58 mentions) [topic]
8. figma (52 mentions) [tool]
9. cloudflare (49 mentions) [tool]
10. electron (44 mentions) [tool]
```

## Activities

```
$ nex-life-logger activities --last 2h --kind youtube

Recent YouTube Activities (last 2 hours)
---
- 2026-04-03 15:41 | Docker in 100 Seconds
  youtube.com/watch?v=Gjnup-PuquQ [transcript available]

- 2026-04-03 14:55 | Building AI Agents with Tool Use
  youtube.com/watch?v=xB2k7... [transcript available]
```
